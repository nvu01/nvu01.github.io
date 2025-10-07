# GitHub Pages Template

A customizable website/blog template powered by [Jekyll](https://jekyllrb.com) and the [Hydejack](https://hydejack.com/) theme. Deploys automatically using GitHub Actions and GitHub Pages.


## Quick Start

### 1. Install Ruby and Jekyll

Follow the official Jekyll installation guide for your operating system:  
🔗 https://jekyllrb.com/docs/installation/

Make sure Ruby, RubyGems, and Bundler are correctly installed before continuing.

### 2. Get the Template

Go to the template repository:

- Click **"Use this template"** (recommended)  
  _or_  
- Fork the repository

### 3. Clone the Repo

Run this command in terminal:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### 4. Install Dependencies
Run this command in the root folder:

```bash
bundle install
```

### 5. Build the Site Locally (optional, for preview)

Make your first edits, then preview the site locally by running:

```bash
bundle exec jekyll serve --livereload
```

- Look for a line like: **Server address: http://127.0.0.1:4000/**
- Open that link in your browser
- Any changes you make will auto-refresh

### 6. Push Your Changes to GitHub

After editing locally, push your changes to trigger deployment:

```bash
git add .
git commit -m "First edits"
git push origin main
```

### 7. Enable GitHub Pages

- Go to Settings → Pages
- Set Source to gh-pages → / (root)
- Click Save
- Wait about 1 minute — your site will be live at: 
**https://\<your-username>.github.io/\<your-repo-name>/**
