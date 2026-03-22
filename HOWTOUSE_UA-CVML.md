# UA-CVML Lab Website Guide

This guide explains how to maintain and update the UA-CVML Lab website. It is intended for future lab members who need to modify the site configuration and content, including the homepage, lab member profiles, projects, publications, alumni, and photos.

The website is built using the **al-folio** Jekyll theme. For additional setup and details, please refer to the following resources:

- [al-folio GitHub Repository](https://github.com/alshedivat/al-folio/tree/main)
- [al-folio Quick Start Guide](https://github.com/alshedivat/al-folio/blob/main/QUICKSTART.md)

## Repository Structure
The website is built using Jekyll with the al-folio theme.
Important folders are listed below.
```
ua-cvml.github.io
├──_bibliography/
    └── papers.bib               # Publication entries (BibTeX)
├── _data/                       # Structured data used by the site
    └── socials.yml              # Social media links and usernames of the web
├── _includes/                   # Reusable HTML/Liquid components
    ├── project_profiles/        # Put Project descriptions
    └── projects.liquid          # for Project component layout
├── _layouts/                    # Page layout templates
├── _pages/                      # Website pages (about, profiles, projects, image, publication, etc.)
├── _projects/                   # Individual member profile files
├── _sass/                       # SASS files defining the website style
    ├── _components.scss         # Reusable component styles (cards, profiles, CV, projects)
    ├── _layout.scss             # Overall layout styles
    ├── _themes.scss             # Theme colors and icons
    └── _variables.scss          # Global variables used by SASS
├── assets/                      # Static files (images, PDFs, media)
    ├── img/
        ├── cvml_lab/            # Put LAB PHOTOS
        ├── people/              # Put Member profile photos
        ├── project/             # Put Project's photos
        └── publication_preview/ # Put Publication preview photos
└── _config.yml                  # Website configuration file
```

## 1. Updating Site Settings
Open the file:
```
_config.yml
```
The following fields control the main site settings:
```yaml
title: blank
first_name: CVML LAB
url: https://ua-cvml.github.io
baseurl: 
```
Notes:
- title – Website title displayed in the browser and navigation bar.
- first_name – Name displayed in the homepage header.
- url – Main website URL.
- baseurl – Leave this empty. Do not delete this field.

## 2. Updating the Homepage
The homepage content is controlled by:
```
_pages/about.md
_layouts/about.liquid
```
You can modify:
- Introduction text
- join_team text
- Selected publications  
  (Publications are automatically selected from: `_bibliography/papers.bib`.  
  A paper will appear on the homepage if it includes: `selected = {true}`)

## 3. Adding a New Lab Member
The **Lab member cards** is located at:
```
_pages/profiles.md
_includes/projects.liquid
```
**Member Photos**  
Place the member’s photo in: `assets/img/people/`  
If no photo is provided, the default image is:`assets/img/people/default_picture.png`  

**Member Profile File**  
Create a new file in: `_projects/`  
Example:`_projects/mingching_project.md`  
Example template:
```yaml
title: Ming-Ching Chang
description: Associate Professor
img: assets/img/people/MingChingChang_19.jpg
importance: 1
category: Lab Co-directors
related_publications: true
redirect: https://www.albany.edu/computer-science/faculty/ming-ching-chang
github: https://github.com/mingching
```
Explanation of fields:
- title – Member name.
- description – Short description shown on the member card.
- img – Path to the member’s profile image.
- importance – Controls the display order of the cards (lower number appears first).
- category – Determines which section the member appears in:
  - Lab Co-directors (for advisors)
  - Lab Members (for students)
- related_publications – If set to true, related publications will be shown
- redirect – External link opened when clicking the member card (optional).
- github – Member’s GitHub profile (optional).

## 4. Adding Publications
The **Publications page** is located at:
```
_pages/publications.md
```
Publication entries are stored in:
```
_bibliography/papers.bib
```
Example entry:
```bibtex
@article{example2025,
  title    = {Example Paper Title},
  author   = {Author A and Author B},
  year     = {2025},
  preview  = {example.png},
  abbr     = {CVPR},
  selected = {true},
  bibtex_show = {true},
}
```
Optional fields:
- selected = {true} → Display the paper on the homepage.
- abbr = {} → Show a venue abbreviation.
- bibtex_show = {true} → Display the BibTeX entry on the site.
- preview = {} → Display a preview image for the publication (Preview images should be stored in: `/assets/img/publication_preview/`).

## 5. Adding Projects
The **Projects page** is located at:
```
_pages/projects.md
_layouts/profiles.liquid
```
Example configuration:
```yaml
  - align: left
    image: project/logo_uumamba.png
    content: project_profiles/about_uumamba.md
    image_circular: false
    more_info: >
      UU-Mamba
    redirect: https://github.com/tiffany9056/UU-Mamba
```
Explanation:
- image – Project image located in: `assets/img/project/` (Optional)
- content – Project description file stored in: `_includes/project_profiles/`
- redirect – Optional link to the project repository or website.

## 6. Adding Alumni
The **Alumni page** is located at:
```
_pages/alumni.md
```
Add new alumni entries directly in this file.

## 7. Adding Photos
Images used in the website gallery are located in:
```
_pages/image.md
```
Photos should be stored in the `assets/img/` directory.

## 8. Other Edits
- **Theme colors**: Edit `_sass/_themes.scss`
- **Social media links**: Edit `_data/socials.yml`
- **Component styles**: Edit `_sass/_components.scss`  
  This file defines the styles for reusable components such as cards, profiles, projects, and CV sections.

## 9. Notes for Future Maintainers
- Always place images inside the assets/img/ directory.
- Maintain consistent formatting when adding members or publications.

View Site (5 min)
1. Go to the ua-cvml.github.io repository → Actions tab
2. Wait for the "Deploy site" workflow to complete (look for a green checkmark, ~4 minutes)
3. Wait for the  Actions tab → All workflows "pages-build-deployment" workflow to complete (look for a green checkmark, ~45 seconds)
4. Visit https://ua-cvml.github.io in your browser

## 10. Deploying with GitHub Pages
The UA-CVML website is hosted with **GitHub Pages**. After changes are pushed to the repository, GitHub will automatically rebuild and deploy the website.

### Steps to deploy
1. Save all file changes.
2. Commit the changes:
   ```bash
   git add .
   git commit -m "Update website content"
   git push origin main
   ```
**After pushing**
- GitHub Pages will automatically start the deployment process.
- The updated website will usually appear within a few minutes.
- You can check the deployment status in the repository under:
  - GitHub Repository → Actions or <br>
  GitHub Repository → Settings → Pages
- If the **[X] Edit lab website: Prettier code formatter** check fails, run the following commands:
    ```bash
    npm install
    npx prettier . --write
    ```

**Notes**
- Make sure all changes are pushed to the correct branch used for deployment.
- If the website does not update, check whether the GitHub Actions workflow failed.
- Common causes of deployment failure include:
  - invalid YAML or Markdown syntax
  - missing included files
  - incorrect image paths
  - Liquid template errors

