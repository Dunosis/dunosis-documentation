# Dunosis Documenation Page

This repository serves as the official docs site for Dunosis.

## Getting Started

Follow these steps to set up the project locally:

### 1. Run the MkDocs Development Server

```bash
mkdocs serve
```
Once the server is running, open your browser and navigate to http://127.0.0.1:8000/ to view the docs site.

### For Additional Info:

Here is the template repository this doumentation site was built upon:

https://github.com/wesordonez/mkdocs-material-template

Here is a documentation of this template repo was created: 

https://jameswillett.dev/getting-started-with-material-for-mkdocs/

And here is additional documentation for Material for MKDocs:

https://squidfunk.github.io/mkdocs-material/getting-started/ 

## Usage Guide
Follow these steps to add Dunosis documentation, guides, instructions, and additional info:

### 1. Create a new branch
Pull most recent main branch to your local development environment and create a new branch titled appropriately. 

```bash
git pull origin main
```

```bash
git checkout -b your-new-branch-name
```

### 2. Add or edit the content

#### Editing Existing Content

To edit existing content, follow these steps:

1. Locate the Markdown file (`.md`) that you want to edit. These files are typically found in the `docs` directory organized by documentation type.
2. Open the file in your preferred text editor.
3. Make the necessary changes to the content. You can edit text, add new sections, update links, etc.
4. Save the changes to the file.
5. Commit the changes with a meaningful commit message.
6. If you are running a local MkDocs server, refresh the page to see the changes. If not, you may need to rebuild the site using the `mkdocs build` command.

#### Adding New Content

To add new content, follow these steps:

1. Create a new Markdown file (`.md`) in the `docs` directory under the appropriate directory by desired section. Name the file appropriately based on the content it will contain.
2. Open the new file in your preferred text editor.
3. Add the content you want to include. Use Markdown syntax to format the text, add headings, lists, links, images, etc.
4. Save the new file.
5. Update the `mkdocs.yml` configuration file to include the new file in the navigation. Add an entry under the `nav` section, specifying the title and the path to the new file. For example:
    ```yaml
    nav:
      - Home: index.md
      - New Page: new_page.md
    ```
6. Commit the new file and the updated configuration file with a meaningful commit message.
7. If you are running a local MkDocs server, refresh the page to see the new content. If not, you may need to rebuild the site using the `mkdocs build` command.
8. Finally, merge into `main` branch and test in the deployed GitHubPages version.

#### Dunosis LLC 2025
