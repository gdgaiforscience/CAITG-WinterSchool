# Build with AI
AI for Science - Build with AI workshop series to supercharge your scientific workflows and pipelines.

Modify `index.qmd` and files in `./sessions` to update the tutorial pages.

Modify `styles.css`, `custom.scss` and `_quarto.yml` to change the look and feel of the rendered pages.

They will be rendered at: https://gdgaiforscience.github.io/Build-with-AI/



## Setting up this repo for auto-building the github pages site

FYI, this only has to be done once. And has already been done. Now just fork this repo or use it as a template when making a new page!

Build the workshop files locally with 
```
git clone  
cd Build-with-AI
quarto render index.qmd 
git commit -am "New build"
git push
```

You must also make a `gh-pages` branch and publish the quarto pages to it locally first. Probably better ways to do this:
```
git checkout -n gh-pages
quarto publish gh-pages
git push origin gh-pages 
git checkout main
```

On the repo turn on github pages at: https://github.com/gdgaiforscience/Build-with-AI/settings/pages
And have it render from `gh-pages` branch.

Add this github action file to render the quarto page on any repo updates. Note any code execution (e.g Python or executable blocks with `{}` syntax will need more installations).
```
name: Quarto Publish

on:
  push:
    branches: main

permissions:
  contents: write
  
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
        with:
          tinytex: true

      - name: Publish to GitHub Pages (and render)
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
          path: .
```
