# 📦 Cyphera's Blog Assets Repository

[![jsDelivr CDN](https://img.shields.io/badge/CDN-jsDelivr-orange)](https://www.jsdelivr.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Repo Size](https://img.shields.io/github/repo-size/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets)](https://github.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets)

Media assets repository for [Cyphera's personal blog](https://cyphera.my.id) - serving images and static files via global CDN for optimal performance.

🚀 **CDN Base URL:** `https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main`

---

## 📁 Repository Structure

```
firmansyahdzakwanarifien-assets/
├── img/
│   ├── posts/          # Images for blog posts
│   │   ├── nfa-certificate.jpg
│   │   ├── cyber-sentinel-cert.jpg
│   │   └── ...
│   ├── projects/       # Screenshots and diagrams for projects
│   │   ├── blankon-infra.png
│   │   ├── devops-pipeline.png
│   │   └── ...
│   ├── album/          # Photos for album/gallery
│   │   ├── nfa-graduation.jpg
│   │   ├── workspace-setup.jpg
│   │   └── ...
│   ├── avatar/         # Profile pictures and avatars
│   │   ├── Logo.png
│   │   └── profile-photo.jpg
│   └── social/         # Social media preview images
│       ├── preview.png
│       └── og-image.jpg
├── docs/               # PDF files, documents
│   └── certificates/
└── README.md          # This file
```

---

## 🚀 CDN Usage

### Base URL Formats

#### jsDelivr (Recommended - Fast & Cached)
```
# Latest (main branch)
https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main/img/posts/image.jpg

# Specific version (immutable, cached forever)
https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@v1.0.0/img/posts/image.jpg

# Specific commit (immutable)
https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@abc123def/img/posts/image.jpg
```

#### Raw GitHub (Slower, not recommended)
```
https://raw.githubusercontent.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets/main/img/posts/image.jpg
```

### Usage Examples

#### In Markdown Posts
```markdown
<!-- Using site.cdn variable (set in _config.yml) -->
![Certificate]({{ site.cdn }}/img/posts/nfa-certificate.jpg)

<!-- Direct URL -->
![Certificate](https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main/img/posts/nfa-certificate.jpg)

<!-- With width attribute -->
![Workspace]({{ site.cdn }}/img/album/workspace.jpg){: width="700" }
```

#### In Front Matter
```yaml
---
title: My Post
image:
  path: /img/posts/featured-image.jpg  # Prepends site.cdn automatically
  alt: Description
---
```

#### In HTML
```html
<img src="https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main/img/posts/image.jpg" 
     alt="Description" 
     width="700">
```

---

## 📤 Upload Workflow

### Method 1: Git CLI (Recommended for Batch)

```bash
# 1. Clone or pull latest
git clone https://github.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets.git
cd firmansyahdzakwanarifien-assets
git pull origin main

# 2. Add your images to appropriate folders
cp ~/Downloads/new-image.jpg img/posts/
cp ~/Photos/event-photo.jpg img/album/

# 3. Optimize images (optional but recommended)
mogrify -strip -quality 85 -resize 1920x1920\> img/posts/new-image.jpg

# 4. Commit and push
git add img/
git commit -m "Add images for [post-name/event]"
git push origin main

# 5. Wait ~5 minutes for CDN propagation
# Or purge cache: https://www.jsdelivr.com/tools/purge
```

### Method 2: GitHub Web Interface (Quick Upload)

1. Navigate to folder: `img/posts/` (or other)
2. Click: **Add file** → **Upload files**
3. Drag & drop images
4. Commit with message: "Add image for [description]"
5. Wait ~5 minutes for CDN

### Method 3: GitHub CLI (Fastest)

```bash
# Single file
gh api repos/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets/contents/img/posts/image.jpg \
  --method PUT \
  --field message="Add new image" \
  --field content=@image.jpg

# Or use gh CLI upload extension
gh repo upload firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets \
  image.jpg \
  --clobber
```

---

## 🎨 Image Guidelines

### File Naming Convention

```bash
# ✅ Good
nfa-graduation-ceremony.jpg
blankon-infrastructure-diagram.png
cyber-sentinel-certificate-2025.jpg

# ❌ Bad
IMG_20251215_143055.jpg
screenshot_final_v2_new.png
photo.jpg
```

**Format:** `descriptive-name-with-dashes.ext`
- Use lowercase
- Separate words with dashes
- Include relevant context (event, project, year)
- No spaces, special characters, or version numbers

### Image Optimization

#### Target Specifications
- **Maximum dimensions:** 1920x1920px
- **Quality:** 85% (JPEG)
- **Format:** 
  - Photos → JPEG
  - Screenshots/Diagrams → PNG
  - Modern browsers → WebP (optional)
- **File size:**
  - Thumbnails: < 100KB
  - Regular posts: < 500KB
  - High-res photos: < 1MB

#### Optimization Commands

```bash
# Compress JPEG (ImageMagick)
mogrify -strip -quality 85 -resize 1920x1920\> image.jpg

# Compress PNG (ImageMagick)
mogrify -strip -define png:compression-level=9 image.png

# Convert to WebP (modern format)
cwebp -q 85 input.jpg -o output.webp

# Batch optimization (all JPEGs in folder)
mogrify -strip -quality 85 -resize 1920x1920\> *.jpg
```

#### Recommended Tools
- **CLI:** ImageMagick, cwebp, jpegoptim, optipng
- **GUI:** [TinyPNG](https://tinypng.com/), [Squoosh](https://squoosh.app/)
- **Automated:** [ImageOptim](https://imageoptim.com/) (Mac), [Trimage](https://trimage.org/) (Linux)

---

## 🔄 CDN Cache Management

### Cache Duration (jsDelivr)
- `@main` branch: 12 hours cache
- `@v1.0.0` version tag: 1 year cache (immutable)
- `@commit-hash`: Permanent cache (immutable)

### Manual Cache Purge

#### Via jsDelivr Purge Tool
```bash
# Purge single file
curl https://purge.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main/img/posts/image.jpg

# Purge all files from main branch
curl https://purge.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main
```

#### Via Web Interface
Visit: https://www.jsdelivr.com/tools/purge

**When to Purge:**
- After replacing an existing image
- After fixing an incorrect upload
- When changes need to be live immediately

**No Need to Purge:**
- New images (not cached yet)
- Using versioned URLs (`@v1.0.0`)
- Using commit-specific URLs

---

## 🏷️ Versioning Strategy

### Development (Rolling Updates)
```yaml
# In main blog _config.yml
cdn: "https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@main"
```
- Always latest images
- 12-hour cache
- Good for active development

### Production (Stable, Immutable)
```bash
# Create version tag
git tag v1.0.0
git push origin v1.0.0

# Update _config.yml
cdn: "https://cdn.jsdelivr.net/gh/firmansyahdzakwanarifien/firmansyahdzakwanarifien-assets@v1.0.0"
```
- Immutable URLs
- 1-year cache
- No surprise changes
- Better for production

### Release Process
```bash
# 1. Test with @main
# 2. When stable, create release
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# 3. Update main blog config to use v1.0.0
# 4. For hotfix, create v1.0.1, etc.
```

---

## 📊 Repository Stats

- **Total Assets:** 150+ images
- **Total Size:** ~145 MB
- **CDN Hits:** Tracked via jsDelivr stats
- **Delivery Speed:** < 100ms globally (via CDN)

---

## 🔒 Security & Access

- **Visibility:** Public repository (required for CDN)
- **Write Access:** Repository owner only
- **CDN Access:** Anyone can access via jsDelivr
- **GitHub Pages:** Not enabled (not needed)

---

## 🤝 Contributing

This is a personal assets repository. If you notice issues:

1. File an issue in the [main blog repo](https://github.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien.github.io/issues)
2. For broken images, provide:
   - URL that's broken
   - Expected image
   - Browser/device info

---


## 🔗 Related Repositories

- **Main Blog:** [firmansyahdzakwanarifien.github.io](https://github.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien.github.io)
- **Theme:** [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)

---

## 📧 Contact

**Firmansyah Dzakwan Arifien**

- 📧 Email: fdzak01@gmail.com
- 🐙 GitHub: [@firmansyahdzakwanarifien](https://github.com/firmansyahdzakwanarifien)

---

<div align="center">

**Powered by jsDelivr CDN**

Fast • Reliable • Global

[Main Blog](https://cyphera.my.id) · [Report Issue](https://github.com/firmansyahdzakwanarifien/firmansyahdzakwanarifien.github.io/issues)

</div>