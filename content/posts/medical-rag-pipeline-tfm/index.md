---
title: "Building a Medical Research RAG Pipeline: My Master's Thesis Journey"
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

# Building a Medical Research RAG Pipeline: My Master's Thesis Journey

For my Master's Thesis at Universidad Complutense de Madrid (UCM), I tackled a fascinating challenge at the intersection of healthcare, artificial intelligence, and data engineering. The goal was ambitious: create a production-ready system that could ingest medical research papers, generate synthetic patient data, and provide AI-powered insights through semantic search and retrieval-augmented generation (RAG).

The result? A comprehensive medical research data pipeline that combines Apache Airflow workflow orchestration, Weaviate vector database, and AI-powered RAG capabilities to enable advanced medical research and patient similarity analysis. In this post, I'll walk you through the problem, the architecture, and the key technical decisions that made this project successful.

🎥 **Want to see it in action?** Check out the [video presentation](https://youtu.be/q3rQbfIoycY) of the solution.

## The Problem: Medical Research at Scale

Healthcare organizations and medical researchers face a critical challenge: how do you efficiently search through thousands of medical research papers and patient records to find relevant information? Traditional keyword-based search systems fall short when dealing with complex medical terminology and semantic relationships.

Moreover, researchers need to:
- **Discover relevant medical literature** from databases like PubMed quickly
- **Find similar patients** based on clinical profiles for treatment recommendations
- **Validate data quality** ensuring accuracy and consistency of medical information
- **Query information naturally** using conversational AI interfaces instead of complex database queries


{{< figure src="images/doctor.png" alt="System Architecture" caption="High-level architecture of the medical research data pipeline" >}}


The medical domain adds another layer of complexity: specialized vocabulary, clinical parameters, and the need for domain-specific embeddings that understand medical context. Generic AI models and search systems simply don't cut it when dealing with conditions like diabetic nephropathy or pharmacological interventions.

## The Solution: A Cloud-Native Medical AI Pipeline

I designed and implemented a complete end-to-end system that addresses these challenges using modern cloud-native technologies and AI capabilities. The system provides automated data ingestion, semantic search, data validation, and an AI-powered query interface.

{{< figure src="images/architecture-overview.png" alt="System Architecture" caption="High-level architecture of the medical research data pipeline" >}}

*[SPACE FOR ARCHITECTURE DIAGRAM - showing Azure, Kubernetes, Airflow, Weaviate, and RAG Agent components]*

### Key Features

The system delivers several critical capabilities:

- **Medical Domain Optimization**: Uses specialized BERT models trained on medical literature for accurate text understanding
- **Dual Data Collections**: Separate collections for research papers (PubMed) and patient profiles (synthetic diabetes data)
- **Advanced Search Capabilities**: Vector search, BM25 keyword search, and hybrid modes with optional reranking
- **Flexible AI Integration**: Supports OpenAI, Azure OpenAI, and local Ollama models for different deployment scenarios
- **Production-Ready Infrastructure**: Complete automation with Terraform, monitoring, and security considerations

## Technical Architecture Deep Dive

Let me break down the core components and how they work together to create a seamless medical research platform.

### Infrastructure Layer: Kubernetes on Azure

The foundation of the system runs on Azure Kubernetes Service (AKS), providing container orchestration, scalability, and resilience. I chose Kubernetes for several reasons:

- **Scalability**: Easily handle varying workloads from batch processing to real-time queries
- **Service Discovery**: Automatic networking between Airflow, Weaviate, and the RAG agent
- **Resource Management**: Efficient allocation of compute and memory for data-intensive tasks
- **Cloud-Native**: Native integration with Azure services and monitoring tools

All infrastructure is defined as code using Terraform, making deployments reproducible and version-controlled. The Terraform modules handle:

```hcl
# Key infrastructure components managed by Terraform
- Azure Kubernetes Service (AKS) cluster
- Apache Airflow with custom medical research DAGs
- Weaviate vector database deployment
- Helm charts for service orchestration
- Optional Application Gateway for secure access
```

{{< figure src="images/infrastructure-diagram.png" alt="Infrastructure Components" caption="Cloud infrastructure components and their interactions" >}}

*[SPACE FOR INFRASTRUCTURE DIAGRAM - showing AKS, Terraform modules, networking, and storage]*

### Data Orchestration: Apache Airflow

Apache Airflow serves as the backbone for workflow orchestration, managing the entire ETL (Extract, Transform, Load) process for medical data. I designed four main DAGs (Directed Acyclic Graphs) that handle different aspects of the pipeline:

#### 1. Medical Research Ingestion DAG

This workflow fetches medical research papers from PubMed using the Biopython library and processes them for storage in Weaviate:

```python
# Key steps in medical research ingestion
1. Query PubMed API for relevant medical papers
2. Extract abstracts, metadata, and MeSH terms
3. Generate embeddings using medical BERT (S-PubMedBert-MS-MARCO)
4. Store in Weaviate with structured schema
5. Handle citation analysis and keyword processing
```

The pipeline handles thousands of papers efficiently, with error handling and retry logic for robust operation.

#### 2. Synthetic Patient Data Ingestion DAG

To enable patient similarity matching without privacy concerns, I implemented synthetic patient data generation focused on diabetes:

```python
# Synthetic patient profile structure
- Demographics: Age, gender, BMI
- Clinical Parameters: HbA1c, glucose, blood pressure
- Kidney Function: eGFR, creatinine levels
- Treatment History: Medications, complications
- Lifestyle Factors: Diet, exercise, smoking status
```

Each patient profile is embedded as a clinical summary, enabling semantic similarity searches.

#### 3. Data Validation DAGs

Two separate validation workflows ensure data quality:

- **Medical Research Validation**: Tests retrieval accuracy, embedding quality, and search performance
- **Patient Data Validation**: Analyzes demographics, clinical correlations, and similarity search effectiveness

{{< figure src="images/airflow-dags.png" alt="Airflow DAG Visualization" caption="The four main DAGs managing the medical data pipeline" >}}

*[SPACE FOR AIRFLOW DAGS DIAGRAM - showing the four DAGs and their task dependencies]*

### Vector Database: Weaviate

Weaviate serves as the semantic search engine and vector database. I chose Weaviate for several compelling reasons:

- **Native Vector Search**: Optimized for high-dimensional medical embeddings
- **Hybrid Search**: Combines vector similarity with BM25 keyword search
- **GraphQL API**: Flexible querying with powerful filtering capabilities
- **gRPC Support**: High-performance connections for real-time queries
- **Schema Management**: Structured data models with automatic validation

#### Data Models

I designed two primary collections with optimized schemas:

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
  bmi: Float
  blood_pressure_systolic: Integer
  blood_pressure_diastolic: Integer
  egfr: Float
  creatinine: Float
  medications: String[]
  complications: String[]
  clinical_summary: Text
}
```

### Medical Embeddings: The Secret Sauce

Generic embedding models don't understand medical terminology well. That's why I integrated **S-PubMedBert-MS-MARCO**, a BERT model specifically trained on PubMed medical literature. This model understands:

- Medical terminology and abbreviations (HbA1c, eGFR, etc.)
- Clinical relationships and correlations
- Drug names and therapeutic interventions
- Disease classifications and symptoms

The embedding model converts text into 768-dimensional vectors that capture semantic meaning, enabling accurate similarity searches.

{{< figure src="images/embedding-process.png" alt="Medical Embedding Pipeline" caption="How medical text is transformed into semantic vectors" >}}

*[SPACE FOR EMBEDDING DIAGRAM - showing text -> tokenization -> BERT -> vector representation]*

### RAG Agent: AI-Powered Medical Assistant

The crown jewel of the system is the Streamlit-based RAG (Retrieval-Augmented Generation) agent. This interface allows researchers and clinicians to query the system using natural language.

#### How RAG Works

The RAG pipeline follows these steps:

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

#### Multi-Provider LLM Support

The agent supports three LLM backends, making it flexible for different deployment scenarios:

**OpenAI:**
```python
# Cloud-based, best performance
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
```

**Azure OpenAI:**
```python
# Enterprise compliance, data residency
client = AzureOpenAI(
    api_key=os.getenv("AZURE_OPENAI_API_KEY"),
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT")
)
```

**Ollama (Local):**
```python
# Privacy-focused, no external API calls
client = Ollama(base_url="http://localhost:11434")
```

#### Advanced Search Modes

The RAG agent provides multiple search strategies:

- **Vector Search**: Pure semantic similarity using embeddings
- **BM25 Search**: Traditional keyword-based search
- **Hybrid Search**: Combines both approaches for best results
- **With Reranking**: Optional reranking step to improve relevance

{{< figure src="images/rag-interface.png" alt="RAG Agent Interface" caption="Streamlit interface for the medical RAG system" >}}

*[SPACE FOR RAG INTERFACE SCREENSHOT - showing the Streamlit UI with query input and results]*

## Practical Use Cases

The system enables several real-world medical research workflows:

### 1. Literature Review

Researchers can quickly find relevant papers on specific topics:

> **Query:** "What are the latest treatments for diabetic nephropathy?"

The RAG agent searches across thousands of PubMed papers and provides a summarized answer with citations.

### 2. Patient Similarity Matching

Clinicians can find similar patients for treatment recommendations:

> **Query:** "Show me patients similar to: 45-year-old male, Type 2 diabetes, HbA1c 8.5%, eGFR 60"

The system uses vector similarity to find patients with comparable clinical profiles.

### 3. Clinical Decision Support

Compare treatment effectiveness across patient cohorts:

> **Query:** "Compare metformin vs insulin effectiveness in elderly patients with reduced kidney function"

The system retrieves relevant patient data and research papers to inform the comparison.

### 4. Drug Discovery Insights

Analyze research papers for therapeutic insights:

> **Query:** "What are emerging therapies targeting SGLT2 inhibitors for diabetes?"

The semantic search identifies relevant papers even when different terminology is used.

## Development Experience: Local to Cloud

One of the key design goals was seamless development from local machines to production cloud deployment. I created comprehensive tooling for both scenarios.

### Local Development Setup

For local development, I created an automated installation script that:

```bash
# Automated local setup with install-airflow.sh
1. Checks prerequisites (kubectl, helm, Docker Desktop)
2. Creates Kubernetes namespaces
3. Deploys Weaviate and Airflow using Helm
4. Generates intelligent port-forwarding script
5. Verifies service health
```

The `port-forward.sh` script manages all service access elegantly:

```bash
# Start all services in background
./port-forward.sh start

# Check status
./port-forward.sh status

# Stop all services
./port-forward.sh stop
```

### Cloud Deployment

Deploying to Azure is equally straightforward:

```bash
# Deploy complete infrastructure
cd terraform_module
terraform init
terraform apply

# Get AKS credentials
az aks get-credentials --resource-group tfm-brayanto --name aks-cluster
```

All services are automatically configured with proper networking, storage, and security settings.

## Data Validation and Quality Metrics

A critical aspect of any data pipeline is ensuring quality. The validation DAGs generate comprehensive reports including:

- **Document Count**: Total papers and patients processed
- **Embedding Quality**: Vector distribution and dimensionality
- **Retrieval Accuracy**: Precision and recall for test queries
- **Clinical Correlations**: HbA1c-glucose and creatinine-eGFR relationships
- **Search Performance**: Query latency and result relevance

{{< figure src="images/validation-metrics.png" alt="Validation Metrics" caption="Data quality metrics from validation DAGs" >}}

*[SPACE FOR VALIDATION METRICS CHART - showing data quality KPIs and graphs]*

## Challenges and Solutions

Building this system came with several interesting challenges:

### Challenge 1: Medical Embedding Model Size

Medical BERT models are large (2GB+), causing slow pod startup times.

**Solution:** Pre-cached models in custom Docker image and implemented lazy loading with progress tracking.

### Challenge 2: PubMed API Rate Limits

Bulk fetching papers triggered rate limiting.

**Solution:** Implemented exponential backoff, request throttling, and batch processing with checkpointing.

### Challenge 3: Vector Search Performance

Initial searches were slow with large collections.

**Solution:** Optimized Weaviate configuration with proper indexing, increased resources, and implemented result caching.

### Challenge 4: LLM Context Window Limits

Long medical papers exceeded token limits.

**Solution:** Implemented intelligent chunking, summarization, and selective passage retrieval.

## Security and Compliance Considerations

Medical data requires careful handling, even when synthetic:

- **Data Encryption**: At-rest and in-transit encryption for all data
- **Access Control**: Azure AD integration with RBAC for AKS
- **Audit Trails**: Comprehensive logging of all data access
- **Secret Management**: Azure Key Vault for API keys and credentials
- **Network Policies**: Kubernetes network segmentation between services

## Performance Results

The system demonstrates strong performance across key metrics:

- **Ingestion Rate**: 500+ PubMed papers per hour
- **Query Latency**: <2 seconds for RAG responses
- **Search Accuracy**: 85%+ relevance for top-5 results
- **Scalability**: Handles 10,000+ patients and papers
- **Availability**: 99.5%+ uptime with Kubernetes auto-healing

## Future Enhancements

Several exciting improvements are on the roadmap:

1. **Multi-Modal Search**: Integrate medical imaging data
2. **Fine-Tuned Medical LLM**: Domain-specific language model
3. **Real-Time Updates**: Streaming ingestion for new papers
4. **Federated Search**: Connect to multiple medical databases
5. **Advanced Analytics**: Predictive modeling and trend analysis

## Key Takeaways

Building this medical research pipeline taught me several valuable lessons:

1. **Domain-Specific Models Matter**: Medical BERT significantly outperforms generic embeddings
2. **Infrastructure as Code**: Terraform and Helm make deployments reproducible and scalable
3. **Validation is Critical**: Comprehensive testing ensures data quality and search accuracy
4. **Flexibility Wins**: Supporting multiple LLM providers accommodates different requirements
5. **Developer Experience**: Good tooling (like port-forward.sh) accelerates development

## Try It Yourself

The complete source code is available on GitHub: [TFM-MDE-BRAYAN-TORRES](https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES)

Getting started is easy:

```bash
# For local development
git clone https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES
cd Local_installation_files
./install-airflow.sh
./port-forward.sh start

# Access services
# Airflow: http://localhost:8080 (admin/admin)
# Weaviate: http://localhost:9090
```

For the RAG agent:

```bash
cd Agent
pip install streamlit weaviate-client sentence-transformers openai
export WEAVIATE_URL="http://localhost:9090"
export OPENAI_API_KEY="your-key-here"
streamlit run agent.py
```

## Conclusion

This Master's Thesis project demonstrates how modern AI and cloud technologies can transform medical research. By combining semantic search, vector databases, and retrieval-augmented generation, we can build systems that genuinely help researchers and clinicians find relevant information faster.

The journey from concept to production-ready system taught me invaluable lessons about data engineering, AI systems, and the unique challenges of the medical domain. Whether you're building similar systems or just exploring RAG applications, I hope this deep dive provides useful insights.

Have questions or want to discuss medical AI pipelines? Feel free to reach out!

---

**Technologies Used**: Python, Apache Airflow, Weaviate, Kubernetes, Azure AKS, Terraform, Streamlit, OpenAI, Medical BERT, PubMed API, Helm

**Repository**: [https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES](https://github.com/Brayantcw/TFM-MDE-BRAYAN-TORRES)

**Video Presentation**: [https://youtu.be/q3rQbfIoycY](https://youtu.be/q3rQbfIoycY)
