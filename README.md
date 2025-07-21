## Quarto Issue: `output-ext` option links are constructed incorrectly

I have a quarto website for a workshop that includes a main webpage
and a folder of slides:

- root
  - index.qmd
  - _quarto.yml
  - slides
    - 01.qmd
    - _metadata.yml


I like having the revealjs slides as well as a one-page HTML document
that students can use to follow along without having to page through
the slides one-by-one.

I finally found the
[`output-ext` rendering option](https://quarto.org/docs/reference/formats/html.html#rendering)
so that all of the qmd files in the slides folder would be built as
slides with `.rjs.html` extension and as HTML webpages with
`.onepage.html` as an extension.
I set this up in a [directory metadata](slides/_metadata.yml) file so
that I didn't have to mess with specifying that in every file.

The problem is that the automatically generated links don't *quite*
work. You can see in the [built page](https://srvanderplas.github.io/reprex-quarto-reveal-site/)
that the Slides link in the navbar goes to
`https://srvanderplas.github.io/reprex-quarto-reveal-site/slides/01.onepage.html.onepage.html`
-- that is, the extension is put on twice.
It should instead link to [this page](https://srvanderplas.github.io/reprex-quarto-reveal-site/slides/01.onepage.html) 
or [the slides](https://srvanderplas.github.io/reprex-quarto-reveal-site/slides/01.rjs.html).

I'm linking to the quarto file in the navbar:

```
  navbar:
    left:
      - href: index.html
        text: Home
      - href: slides/01.qmd
        text: Slides
```

Now, it would also be nice to be able to specify a stub at the 
end of the file, rather than just an extension 
(extra dots in filenames drive me nuts),
but even as it's currently configured, something isn't quite working
correctly.

When `navigate: true` is enabled in the project options, this becomes 
even more irritating, since a window pops up and gives you a 404 or 
a missing resource warning.

Desired outcome(s): 

- Link to `https://srvanderplas.github.io/reprex-quarto-reveal-site/slides/01.onepage.html`
- Allow the user to specify which format to prefer when linking to qmd files, 
preferably on a directory level.
- Provide a `output-stub` option instead or in addition to `output-ext` so that 
the user doesn't have to add a pseudo-extension to differentiate reveal files 
from regular HTML files. 




