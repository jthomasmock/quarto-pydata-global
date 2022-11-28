## Outline

# Quarto

## Jupyter Tradeoffs

> Jupyter notebooks are notebooks. Jupyter is the product. Quarto notebooks are just plain text .qmd documents.

- Jupyter requires special UI (Jupyter/Lab, VS Code)
- JSON behind the scenes, stores state and source code in same document
- Hidden state and out-of-order execution
- JSON has issues with version control

## RMarkdown Tradeoffs
- Requires R
- Requires linear execution, top to bottom
- Doesn't have global cache - specific to single file

## Quarto tradeoffs
- Offers special UIs (RStudio and VS Code), but can be written in ANY text editor, and can be edited in Version Control
- Doesn't require the use of plain text (could be ALL ipynb) but to an extent optimizes for plain text
- 3 separate files:
  - Source Code
  - Output file (HTML/PDF/etc)
  - Frozen output (JSON)
- Requires linear execution, top to bottom
- Import code OR other documents
- Combine any number of inputs, such as .ipynb, .qmd, .rmd, .md, .txt, .css, .html, etc.
- Easy to reprex as source code is raw text
- Can keep errors in the document and can include/style non-executed chunks

## nbdev Enhances Jupyter
- Better source control editing
- Develop python packages with Notebooks
- nbdev uses Quarto for websites/rendering

## nbconvert

- nbconvert focuses on ipynb -> other file types via Pandoc
- n
- Quarto converts various input types -> other file types via Pandoc

## Templates

Expectation that you're likely writing a good amount of jinja templates, raw HTML, raw LaTeX, or templates

```python
from jinja2 import DictLoader

dl = DictLoader({'footer':
"""
{%- extends 'lab/index.html.j2' -%}

{% block footer %}
FOOOOOOOOTEEEEER
{% endblock footer %}
"""})


exportHTML = HTMLExporter(extra_loaders=[dl], template_file='footer')
(body, resources) = exportHTML.from_notebook_node(jake_notebook)
for l in body.split('\n')[-4:]:
    print(l)
```

## Quarto Templates

Quarto builds in templates for almost everything and for the core use cases EVERYTHING is markdown.

````markdown

---
title: My example
author: Tom Mock
---

## First Chapter

Let's write some _rich_ **text** with [links](https://quarto.org) and lists:

1. Item 1
1. Item 2
  1. Subitem
  1. Subitem
1. Item 3

```{python}
from plotnine import ggplot, geom_point, aes, stat_smooth, facet_wrap
from plotnine.data import mtcars

(ggplot(mtcars, aes('wt', 'mpg', color='factor(gear)'))
 + geom_point()
 + stat_smooth(method='lm')
 + facet_wrap('~gear'))
```

````
