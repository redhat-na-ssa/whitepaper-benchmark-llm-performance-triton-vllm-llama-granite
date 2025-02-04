# Example using pandoc

[Example Document](EXAMPLE.md)

RHEL / Fedora

```sh
dnf install -y pandoc pdflatex texlive-ec
```

```sh
pandoc \
  EXAMPLE.md \
  --from=markdown \
  --output=example.tex \
  --to=latex \
  --standalone
```

```sh
pandoc \
  EXAMPLE.md \
  --from=markdown \
  --output=example.pdf
```

## Reference

- https://tex.stackexchange.com/questions/101717/converting-markdown-to-latex-in-latex#246871