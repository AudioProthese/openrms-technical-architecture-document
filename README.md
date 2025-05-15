# Technical Architecture Document Repository

## How to build locally

Edit the `TAD.md` file and run the following command to build the document (using Docker):

```bash
docker run --rm -v "$PWD":/data -w /data pandoc/extra:3.7.0-ubuntu \
  pandoc TAD.md -o TAD.pdf \
    --template=eisvogel \
    --pdf-engine=xelatex \
    --listings \
    --number-sections
```

Refer to [Eisvogel](https://github.com/enhuiz/eisvogel) template documentation for more customization options.
