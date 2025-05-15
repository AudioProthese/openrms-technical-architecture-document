# Technical Architecture Document Repository

Edit the `TAD.md` file, push it to the repository. You can then retrieve the PDF version of the document from the CI/CD pipeline's artefacts.

## How to build locally

Edit the `TAD.md` file and run the following command to build the document (using Docker):

```bash
docker run --rm -v "$PWD":/data -w /data pandoc/extra:3.7.0-ubuntu \
    TAD.md -o TAD.pdf \
    --template=eisvogel \
    --pdf-engine=xelatex \
    --listings \
    --number-sections
```

Refer to [Eisvogel](https://github.com/enhuiz/eisvogel) template documentation for more customization options.
