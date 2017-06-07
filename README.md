# pandoc-mkdocs

[![](https://images.microbadger.com/badges/image/silentstorm/pandoc-mkdocs.svg)](https://microbadger.com/images/silentstorm/pandoc-mkdocs "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/silentstorm/pandoc-mkdocs.svg)](https://microbadger.com/images/silentstorm/pandoc-mkdocs "Get your own version badge on microbadger.com")

This is a docker image made for GitLab-CI. It contains mkdocs as well as pandoc with LaTeX(for pdf support).
Besides that it contains a helper script that uses the mkdocs.yml to merge all the markdown files from your documentation into
one single file which can be used by pandoc to generate a pdf-file of your documentation.
Imagemagick is also contained which helps you change images before creation of the mkdocs-site or the pdf.

Even though the `latest`-tag image is based on debian it doesn't contain the packaged version from the debian repository but version `1.19.2.1` of pandocs from their download page.

## Example

A .gitlab-ci using this image could look like this:

```YAML
image: silentstorm/pandoc-mkdocs
    
generate_documentation_pdf:
  stage: deploy
  script:
  - mkdocscombine -o asPandoc.pd
  - pandoc --toc --latex-engine=xelatex -f markdown+grid_tables+table_captions -o Dokumentation.pdf asPandoc.pd
  artifacts:
    paths:
    - "Dokumentation.pdf"
    
build_documentation:
  stage: build
  script:
  - mkdocs build
  artifacts:
    paths:
    - "site/"
```

