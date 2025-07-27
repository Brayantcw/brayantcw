# Brayant Torres - Tech Blog

A modern tech blog built with Hugo and the PaperMod theme, hosted on GitLab Pages.

## 🚀 About

This is my personal tech blog where I share insights about software development, programming tutorials, and technology trends. Built with Hugo for speed and simplicity, styled with the beautiful PaperMod theme.

## 🛠️ Tech Stack

- **Static Site Generator**: [Hugo](https://gohugo.io/)
- **Theme**: [PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- **Hosting**: GitLab Pages
- **CI/CD**: GitLab CI

## 📝 Blog Topics

- Programming tutorials and guides
- Software engineering best practices
- Technology reviews and analysis
- Project showcases and case studies
- Career insights and experiences

## 🏗️ Development

### Prerequisites

- [Hugo Extended](https://gohugo.io/getting-started/installing/) (v0.146.0+)
- [Git](https://git-scm.com/)

### Local Development

1. Clone the repository:
   ```bash
   git clone https://gitlab.com/brayantcw/brayantcw.git
   cd brayantcw
   ```

2. Initialize and update the theme submodule:
   ```bash
   git submodule update --init --recursive
   ```

3. Start the development server:
   ```bash
   hugo server -D
   ```

4. Open your browser and visit `http://localhost:1313`

### Creating New Posts

Create a new blog post:
```bash
hugo new posts/my-new-post.md
```

### Building for Production

Build the static site:
```bash
hugo --minify
```

The generated site will be in the `public/` directory.

## 📁 Project Structure

```
├── .gitlab-ci.yml          # GitLab CI/CD configuration
├── .gitignore              # Git ignore rules
├── config.yaml             # Hugo configuration
├── content/                # Content directory
│   ├── posts/              # Blog posts
│   ├── about.md            # About page
│   └── search.md           # Search page
├── static/                 # Static assets
│   └── images/             # Images
├── themes/                 # Hugo themes
│   └── PaperMod/           # PaperMod theme (git submodule)
└── README.md               # This file
```

## 🎨 Theme Features

The PaperMod theme includes:

- ⚡ Fast and lightweight
- 🌓 Light/Dark mode toggle
- 📱 Fully responsive design
- 🔍 Built-in search functionality
- 📊 Reading time and word count
- 🏷️ Tags and categories support
- 📱 Social media share buttons
- 💬 Comments support (configurable)
- 🎯 SEO optimized

## 🚀 Deployment

The blog is automatically deployed to GitLab Pages using GitLab CI/CD:

- **Production**: Pushes to `main` branch trigger deployment
- **Testing**: Other branches run build tests without deployment
- **URL**: https://brayantcw.gitlab.io/brayantcw

### Manual Deployment

To deploy manually:

1. Build the site: `hugo --minify`
2. The `public/` directory contains the deployable files

## 📞 Contact

- **GitHub**: [@brayantcw](https://github.com/brayantcw)
- **LinkedIn**: [Brayant Torres](https://linkedin.com/in/brayant-torres)
- **Twitter**: [@brayantcw](https://twitter.com/brayantcw)
- **Blog**: [brayantcw.gitlab.io/brayantcw](https://brayantcw.gitlab.io/brayantcw)

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

While this is a personal blog, I welcome suggestions and improvements:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a merge request

---

Built with ❤️ by Brayant Torres