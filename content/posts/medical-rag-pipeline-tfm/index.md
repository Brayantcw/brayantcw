---
title: "Production-Ready Medical AI: A Deep Dive into RAG Pipelines for Healthcare"
date: 2025-10-25T12:00:00-00:00
draft: false
tags: ["ai", "rag", "medical-ai", "kubernetes", "airflow", "weaviate", "machine-learning", "data-engineering"]
categories: ["ai", "data-engineering"]
author: "Brayant Torres"
description: "How I built a comprehensive medical research data pipeline combining Apache Airflow, Weaviate vector database, and RAG capabilities to enable advanced medical research and patient similarity analysis."
cover:
    image: "<image path/url>"
    alt: "<alt text>"
    caption: "<text>"
    relative: false
    hidden: true
showToc: true
TocOpen: false
hidemeta: false
comments: false
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
editPost:
    URL: "https://github.com/brayantcw/brayantcw/edit/main/content"
    Text: "Suggest Changes"
    appendFilePath: true
---

# Production-Ready Medical AI: A Deep Dive into RAG Pipelines for Healthcare

When I started my Master's Thesis at Universidad Complutense de Madrid, I knew I wanted to work on something that really mattered. I ended up diving deep into a problem that sits right at the sweet spot of healthcare, AI, and data engineering: how do we make medical research more accessible and actionable?

The challenge? Build a system that could actually work in the real world—one that ingests medical research papers, generates synthetic patient data, and delivers intelligent insights through semantic search and RAG (Retrieval-Augmented Generation).

After months of work (and plenty of late nights debugging Kubernetes pods), I built a medical research data pipeline that brings together Apache Airflow for orchestration, Weaviate as a vector database, and RAG capabilities for AI-powered analysis. The system helps researchers find relevant studies and identify similar patient cases way faster than traditional methods.

In this post, I'm going to break down the problem I was trying to solve, the architecture I designed, and some of the key decisions I made along the way. Spoiler alert: it involved a lot of trial and error, but that's where the interesting lessons are.

## The Problem: Why Medical Research Needs Better Tools

If you've ever tried searching for medical information, you know how frustrating it can be. Now imagine you're a researcher trying to sift through thousands of research papers and patient records to find what you need. Traditional search tools—the ones that just look for keyword matches—really struggle here. Medical terminology is complex, and context matters a lot.

Here's what researchers actually need to do every day:
- **Find relevant studies fast** – PubMed has millions of papers, and time matters when you're treating patients
- **Identify similar patient cases** – knowing how other patients with similar profiles responded to treatment can be incredibly valuable
- **Trust the data** – medical information needs to be accurate and consistent
- **Ask questions naturally** – nobody wants to learn complex database query languages when they could just ask a question in plain English

But here's where it gets tricky: medical language is its own beast. You can't just throw a general-purpose AI at terms like "diabetic nephropathy" or expect it to understand the nuances of different pharmacological interventions. The medical domain needs specialized tools that actually understand clinical context—not just pattern matching on buzzwords.

That's the gap I wanted to fill.

## The Solution: Building Something That Actually Works

So I rolled up my sleeves and built an end-to-end system to tackle these problems. The key was using modern cloud-native tools and AI in a way that made sense for the medical domain—not just because they're trendy, but because they solve real problems.

What I ended up with is a pipeline that handles everything: it automatically pulls in data, understands what it means (thanks to semantic search), validates accuracy, and lets researchers ask questions like they're talking to a colleague instead of a database.

{{< figure src="images/alto_nivel.png" alt="System Architecture" caption="High-level architecture of the medical research data pipeline" >}}

### What It Can Do

Here's what makes this system tick:

- **Medical Domain Optimization** – I used specialized BERT models that were actually trained on medical literature. This makes a huge difference when dealing with clinical terminology.
- **Dual Data Collections** – Separate spaces for research papers (from PubMed) and patient profiles (synthetic diabetes data, because getting real patient data is... complicated).
- **Multiple Search Strategies** – Vector search for semantic similarity, BM25 for keyword matching, and hybrid modes that combine both. Plus optional reranking to fine-tune results.
- **Flexible AI Backend** – Works with OpenAI, Azure OpenAI, or local Ollama models depending on your needs and budget.
- **Production-Ready Setup** – Everything automated with Terraform, complete with monitoring and security baked in.

## Getting Into the Technical Details

Let me walk you through how this all fits together. Fair warning: we're about to get into the weeds a bit.

### The Foundation: Kubernetes on Azure

The whole system runs on Azure Kubernetes Service (AKS). I went with Kubernetes for a few good reasons:

- **It scales when you need it** – Whether you're running batch jobs or handling real-time queries, K8s handles it
- **Services talk to each other automatically** – No manual configuration for networking between Airflow, Weaviate, and the AI agent
- **Smart resource management** – When you're dealing with embedding models and large datasets, efficient compute allocation matters
- **Cloud-native integrations** – Azure plays nice with Kubernetes, making monitoring and management easier

Everything is infrastructure-as-code using Terraform. This was a game-changer for reproducibility. I can spin up the entire stack with a single command, and everything is version-controlled:

```hcl
# Key infrastructure components managed by Terraform
- Azure Kubernetes Service (AKS) cluster
- Apache Airflow with custom DAGs
- Weaviate vector database deployment
- Application Gateway for secure access
- Azure Storage Accounts for persistent storage
```

{{< figure src="images/Arquitectura.png" alt="Infrastructure Components" caption="Cloud infrastructure components and their interactions" >}}

### The Orchestrator: Apache Airflow

Apache Airflow is the brain of the operation. It manages all the ETL workflows for getting data in, processing it, and keeping it fresh. I built four main DAGs that each handle different pieces:

#### 1. Getting Medical Research Papers

This workflow pulls papers from PubMed using the Biopython library and gets them ready for Weaviate:

```python
# Key steps in medical research ingestion
1. Query PubMed API for relevant medical papers
2. Extract abstracts, metadata, and MeSH terms
3. Generate embeddings using medical BERT (S-PubMedBert-MS-MARCO)
4. Store in Weaviate with structured schema
5. Handle citation analysis and keyword processing
```

It can process thousands of papers, and I added retry logic so it doesn't break when the PubMed API has a bad day.

{{< figure src="images/medical_ingestion.png" alt="DAG medical Ingestion" caption="Medical Ingestion Dag" >}}

#### 2. Creating Synthetic Patient Data

Here's a fun part: to enable patient similarity matching without dealing with privacy regulations (or the nightmare of getting access to real patient data), I built a synthetic data generator focused on diabetes patients:

```python
# Synthetic patient profile structure
- Demographics: Age, gender, BMI
- Clinical Parameters: HbA1c, glucose, blood pressure
- Kidney Function: eGFR, creatinine levels
- Treatment History: Medications, complications
- Lifestyle Factors: Diet, exercise, smoking status
```
{{< figure src="images/sysntethic_data_ingestion.png" alt="DAG patient Data Generator" caption="Synthetic Patient Data Ingestion DAG" >}}

Each patient profile gets turned into a clinical summary and embedded, so we can do semantic searches to find similar cases.

{{< figure src="images/patient.png" alt="patient" caption="Vector representation of patient data" >}}

#### 3. Making Sure the Data is Good

I built two separate validation pipelines because data quality in healthcare is non-negotiable:

**Medical Research Validation** – Tests whether we're getting accurate retrieval, good embedding quality, and fast search performance.

{{< figure src="images/val_article.png" alt="validation article" caption="Research Paper Validation Pipeline" >}}

**Patient Data Validation** – Checks demographics make sense, clinical parameters correlate properly, and similarity searches actually work.

{{< figure src="images/val_patient.png" alt="validation patient" caption="Patient Data Validation Pipeline" >}}

### The Search Engine: Weaviate

Weaviate is where all the magic happens for search. I picked it over other vector databases for some pretty compelling reasons:

- **Built for vector search** – It's optimized specifically for high-dimensional embeddings like the ones we're using for medical text
- **Hybrid search out of the box** – Combines vector similarity with BM25 keyword search, giving you the best of both worlds
- **GraphQL API** – Makes querying flexible and powerful
- **Fast performance** – gRPC support means real-time queries don't feel sluggish
- **Structured data models** – You can define schemas and get automatic validation

#### How I Set Up the Data

I designed two main collections with schemas that make sense for the data:

**MedicalResearch Collection:**
```graphql
{
  title: String
  abstract: Text
  pmid: String
  journal: String
  authors: String[]
  publication_date: Date
  mesh_terms: String[]
  citation_count: Integer
}
```

**DiabetesPatients Collection:**
```graphql
{
  patient_id: String
  age: Integer
  gender: String
  hba1c: Float
  glucose_level: Float
  egfr: Float
  medications: String[]
  complications: String[]
}
```

### The User Interface: RAG Agent

This is the part users actually interact with—a Streamlit app that lets researchers ask questions in plain English and get intelligent answers back.

#### How RAG Works Here

The pipeline is pretty straightforward:

```python
# RAG Pipeline Flow
1. User submits a natural language question
2. Question is embedded using the medical BERT model
3. Weaviate performs semantic search across collections
4. Top-k relevant documents are retrieved
5. Documents + question are sent to LLM as context
6. LLM generates informed answer based on retrieved data
7. Answer is presented to user with source citations
```

#### Different Ways to Search

I implemented multiple search strategies because different queries need different approaches:

- **Vector Search** – Pure semantic similarity. Great for conceptual questions.
- **BM25 Search** – Traditional keyword matching. Works well when you know exact terms.
- **Hybrid Search** – Combines both. Usually the best option.
- **With Reranking** – An optional step that reorders results for even better relevance.

{{< figure src="images/Articles.png" alt="RAG Agent Interface" caption="Streamlit interface for the medical RAG system" >}}

## What You Can Actually Do With This

Theory is great, but let's talk about real use cases:

### Literature Review Made Easy

Say you're a researcher trying to catch up on the latest treatments:

> **Query:** "What are the latest treatments for diabetic nephropathy?"

The RAG agent searches thousands of PubMed papers and gives you a summary with citations. No more spending hours skimming abstracts.

### Finding Similar Patients

Clinicians can find comparable cases for treatment insights:

> **Query:** "Show me patients similar to: 45-year-old male, Type 2 diabetes, HbA1c 8.5%, eGFR 60"

The system uses vector similarity to find patients with matching clinical profiles. It's like having a photographic memory of every case you've ever seen.

### Clinical Decision Support

Compare different treatment approaches:

> **Query:** "Compare metformin vs insulin effectiveness in elderly patients with reduced kidney function"

The system pulls relevant patient data and research papers to help inform the comparison.

### Research Insights

Analyze papers for emerging trends:

> **Query:** "What are emerging therapies targeting SGLT2 inhibitors for diabetes?"

Even if papers use different terminology, semantic search finds what you're looking for.

## From Laptop to Cloud: Making Development Smooth

I wanted this to be easy to work with, whether you're developing locally or deploying to production. So I built tooling for both scenarios.

### Working Locally

For local development, I created an automated setup script:

```bash
# Automated local setup with install-airflow.sh
1. Checks prerequisites (kubectl, helm, Docker Desktop)
2. Creates Kubernetes namespaces
3. Deploys Weaviate and Airflow using Helm
4. Generates intelligent port-forwarding script
5. Verifies service health
```

The port-forward script makes accessing services simple:

```bash
# Start all services in background
./port-forward.sh start

# Check what's running
./port-forward.sh status

# Stop everything
./port-forward.sh stop
```

### Deploying to Azure

Getting everything running in the cloud is just as straightforward:

```bash
# Deploy complete infrastructure
cd terraform_module
terraform init
terraform apply

# Connect to your cluster
az aks get-credentials --resource-group tfm-brayanto --name aks-cluster
```

Everything gets configured automatically—networking, storage, security, the works.


## How Well Does It Work?

The system performs pretty well across the metrics that matter:

- **Ingestion Speed** – Processes 500+ PubMed papers per hour
- **Query Response Time** – Under 2 seconds for RAG answers
- **Search Relevance** – 85%+ accuracy for top-5 results
- **Scale** – Handles 10,000+ patients and papers without breaking a sweat
- **Reliability** – 99.5%+ uptime thanks to Kubernetes auto-healing

## What's Next?

There's always room to make things better. Here's what I'm thinking about:

1. **Multi-Modal Search** – Add support for medical imaging data
2. **Fine-Tuned Medical LLM** – Train a domain-specific language model
3. **Real-Time Updates** – Stream new papers as they're published
4. **Federated Search** – Connect to multiple medical databases simultaneously
5. **Predictive Analytics** – Add modeling for trend analysis and predictions


## Want to Try It?

The complete source code is on GitHub: [TFM-MDE-BRAYAN-TORRES](https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES)

Feel free to clone it, break it, improve it—whatever works for you.

## Wrapping Up

This Master's Thesis showed me how powerful modern AI and cloud technologies can be when applied thoughtfully to real problems. By combining semantic search, vector databases, and retrieval-augmented generation, we can build systems that genuinely help people do their jobs better.

The journey from "wouldn't it be cool if..." to a production-ready system taught me more than any course could. Whether you're building something similar or just exploring what's possible with RAG, I hope this breakdown gives you some useful insights.

---

**Repository**: [https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES](https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES)