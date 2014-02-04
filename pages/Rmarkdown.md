---
layout: page
title: Knitr with R Markdown
---

The simplest way to write a quick report, mixing in a bit of R, is to
use [R Markdown](http://www.rstudio.com/ide/docs/r_markdown), a
variant of [Markdown](http://daringfireball.net/projects/markdown/)
developed by the folks at [Rstudio](http://www.rstudio.com).

[Markdown](http://daringfireball.net/projects/markdown/) is a system
for writing simple, readable text, with the sort of marks that you'd
use in an email message (for example, `**bold**` for **bold** or
`_italics_` for _italics_), that can be easily converted to
[html](http://en.wikipedia.org/wiki/HTML).

### HTML

It's helpful to know a bit of html, which is the markup language that
web pages are written in. html really isn't that hard; it's just
cumbersome.

An html document contains pairs of tags to indicate content, like
`<h1>` and `</h1>` to indicate that the enclosed text "level one
header", or `<em>` and `</em>` to indicate emphasis (generally
_italics_). A web browser will
[parse](http://en.wikipedia.org/wiki/Parsing) the html tags and render
the web page, often using a
[Cascading style sheet (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets)
to define the precise style of the different elements.

But we won't get into all of that; html is great, but the code is
cumbersome to create directly, as it looks something like this:

    <!DOCTYPE html>
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    </head>

    <body>
    <h1>Markdown example</h1>
    
    <p>This is a simple example of a Markdown document.</p>
    
    <p>Use a blank link between paragraphs.
    You can use a bit of <strong>bold</strong> or <em>italics</em>. Use backticks to indicate
    <code>code</code> that will be rendered in monospace.</p>
    
    <p>Here's a list:</p>
    
    <ul>
    <li>an item in the list</li>
    <li>another item</li>
    <li>yet another item</li>
    </ul>
    
    <p>You can include blocks of code using three backticks:</p>
    
    <p><code>
    x &lt;- rnorm(100)
    y &lt;- 2*x + rnorm(100)
    </code></p>
    
    <p>Or you could indent four spaces:</p>
    
    <pre><code>mean(x)
    sd(x)
    </code></pre>
    
    <p>It'll figure out numbered lists, too:</p>
    
    <ol>
    <li>First item</li>
    <li>Second item</li>
    </ol>
    
    <p>And it's easy to create links, like to
    the <a href="http://daringfireball.net/projects/markdown/">Markdown</a>
    page.</p>
    </body>
    </html>

Pretty ugly. That's probably more than you really needed to see. But
knowing about html gives you a greater appreciation of Markdown.

### Markdown

As I mentioned above,
[Markdown](http://daringfireball.net/projects/markdown/) is a system
for writing simple, readable text that is easily converted into
html. The reason it's useful to know a bit of html is that then you
have a better idea how the final product will look. (Plus, if you want
to get fancy, you can just insert a bit of html within the Markdown
document.)

A Markdown document looks like this:

    # Markdown example

    This is a simple example of a Markdown document.

    Use a blank link between paragraphs.
    You can use a bit of **bold** or _italics_. Use backticks to indicate
    `code` that will be rendered in monospace.

    Here's a list:

    - an item in the list
    - another item
    - yet another item

    You can include blocks of code using three backticks:

    ```
    x <- rnorm(100)
    y <- 2*x + rnorm(100)
    ```

    Or you could indent four spaces:

        mean(x)
        sd(x)
    
    It'll figure out numbered lists, too:

    1. First item
    2. Second item

    And it's easy to create links, like to
    the [Markdown](http://daringfireball.net/projects/markdown/)
    page.

That bit of Markdown text gets converted to the html code in the
previous section.

I hope the markup is reasonably self-explanatory. Markdown is just a
system of marks that will get searched-and-replaced to create an html
document.

Here's a
[more extensive example](http://www.unexpected-vortices.com/sw/gouda/quick-markdown-example.html).
Or look at the [Markdown basics](http://daringfireball.net/projects/markdown/basics) page, 
and the more complete [Markdown syntax](http://daringfireball.net/projects/markdown/syntax), 
or just the [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

### R Markdown

[R Markdown](http://www.rstudio.com/ide/docs/r_markdown), a
variant of [Markdown](http://daringfireball.net/projects/markdown/)
developed by the folks at [Rstudio](http://www.rstudio.com): It's
Markdown with embedded [R](http://www.r-project.org) code chunks, to
be used with [knitr](http://yihui.name/knitr/) to make it easy to
reproducible web-based reports. The Markdown syntax has some
enhancements (see the
[R Markdown page](http://www.rstudio.com/ide/docs/r_markdown)), and
you can include LaTeX equations (see the
[Equations in R Markdown](http://www.rstudio.com/ide/docs/authoring/using_markdown_equations)).

Here's an [example R Markdown document](../assets/knitr_example.Rmd),
and the [html document it produces](../assets/knitr_example.html).

#### Code chunks

The key thing for us to focus on are the code chunks, which look like this:

    ```{r simulate_data}
    x <- rnorm(100)
    y <- 2*x + rnorm(100)
    ```

In the midst of an otherwise plain Markdown document, you'll have a
bit of R code that is initiated by a line like this

    ```{r chunk_name}

After the code, there'll be a line with just three backticks.

    ```

The initial line may also include various options. For example, `echo=FALSE`
indicates that the code will not be shown in the final document
(though any results/output would still be displayed).

    ```{r chunk_name, echo=FALSE}
    x <- rnorm(100)
    y <- 2*x + rnorm(100)
    cor(x, y)
    ```
    
You use `results="hide"` to hide the results/output (but here the code
would still be displayed).

    ```{r chunk_name, results="hide"}
    x <- rnorm(100)
    y <- 2*x + rnorm(100)
    cor(x, y)
    ```
    
You use `include=FALSE` to have the chunk _evaluated_, but neither the
code nor its output will be displayed.

    ```{r chunk_name, include=FALSE}
    x <- rnorm(100)
    y <- 2*x + rnorm(100)
    cor(x, y)
    ```

If I'm writing a report for a collaborator, I'll often use
`include=FALSE` to suppress all of the code and largely just include
figures.

For figures, you'll want to use options like `fig.width` and
`fig.height`. For example:

    ```{r scatterplot, fig.width=8, fig.height=6}
    plot(x,y)
    ```

When you process the R Markdown document with knitr, each of the code
chunks will be evaluated, and then the code and/or output will be
inserted (unless you suppress one or both with the options above). If
the code produces a figure, that figure will be inserted.

An R Markdown document will have often have _many_ code chunks. They are
evaluated in order, in a single R session, and the state of the
various variables in one code chunk are preserved in future chunks.

There are
[lots of different possible "chunk options"](http://yihui.name/knitr/options#chunk_options). 
Each must be real R code, as R will be used to evaluate them. So
`results=hide` is wrong; you need `results="hide"`

#### Global chunk options

You may be inclined to use largely the same set of chunk options
throughout a document. That'd be a pain. Thus, you want to set some
global chunk options at the top of your document.

For example, I might use `include=FALSE` or at least `echo=FALSE`
globally for a report to a scientific collaborator who wouldn't want
to see all of the code. And I might want something like `fig.width=12`
and `fig.height=6` if I generally want those sizes for my figures.

I'd set such options by having an initial code chunk like this:

    ```{r global_options, include=FALSE}
    opts_chunk$set(fig.width=12, fig.height=8, fig.path='Figs/',
                   echo=FALSE, warning=FALSE, message=FALSE)
    ```

I snuck a few additional options in there: `warning=FALSE` and
`message=FALSE` suppresses any warnings or messages from being included in
the final document, and `fig.path='Figs/'` makes it so the figures
produced get placed in the `Figs` subdirectory. (By default, they'd go
in a subdirectory called `figure/`, and `Figs` is more my style.) 

**Note**: the ending slash in `Figs/` is critical. If you used
`fig.path='Figs'` then the figures would go in the main directory but
with `Figs` as the initial part of their name.

The global chunk options become the defaults for the rest of the
document. Then if you want a particular chunk to have a different
behavior, for example, to have a different figure height, you'd use
define a different option within that chunk. For example:

    ```{r a_taller_figure, fig.height=32}
    par(mfrow=c(8,2))
    for(i in 1:16)
      plot(x[,i], y[,i])
    ```

In a report to a collaborator, I might use `include=FALSE, echo=FALSE`
as a global option, and then use `include=TRUE` for the chunks that
produce figures. Then the code would be suppressed throughout, and any output
would be suppressed except in the figure chunks (where I used
`include=TRUE`), which would produce just the figures.

#### Package options

In addition to the chunk options, there are also
[package options](http://yihui.name/knitr/options#package_options),
set with something like:

    ```{r package_options, include=FALSE}```
    opts_knit$set(progress = TRUE, verbose = TRUE)
    ```

I was confused about this at first: I'd use `opts_knit$set` when I
really wanted `opts_chunk$set`.  knitr includes _a lot_ of options; if
you're getting fancy you may need these package options, but initially
you'd just be using the chunk options and, particularly, the global
chunk options defined via `opts_chunk$set`.


#### In-line code
    
A key motivation for knitr is
[reproducible research](http://en.wikipedia.org/wiki/Reproducibility#Reproducible_research):
that our results are accompanied by the data and code needed to
produce them.

Thus, your report should never explicitly include numbers that are 
derived from the data. You'd never say "There are 168 individuals."
Rather, you'd insert in place of the 168 a bit of code that, when
evaluated, gives the number of individuals.

That's the point of the in-line code. You'd write something like this:

    There are `r nrow(my_data)` individuals.

Another example:

    The estimated correlation between x and y was `r cor(x,y)`.
    
In R Markdown, in-line code is indicated with `` `r  `` and `` ` ``.
The bit of R code between them is evaluated and the result inserted.    

**An important point**: you need to be sure that these in-line bits of
code aren't split across lines in your document. Othewise you'll just
see the raw code and not the result that you want.
cor(x,y).

#### Rounding

I'm very particularly about the rounding of results. If I've estimated
a correlation coefficient with 1000 data points, I don't want to see
`0.9032738`. I want `0.90`.

You could use the R function `round`, like this: `` `r round(cor(x,y), 2)`.
But that would produce `0.9` instead of `0.90`.

One solution is to use the `sprintf` function, like so:
`` `r sprintf("%.2f", cor(x,y))` ``. That's perfectly reasonable,
right? Well, it is if you're a C programmer.

But a problem arises if the value is `-0.001`. `` `r sprintf("%.2f", -0.001)`
will produce `-0.00`. I don't like that, nor does 
[Hilary](https://twitter.com/hspter/status/314858331598626816).

My solution to this problem is the
[`myround`](https://github.com/kbroman/broman/blob/master/R/myround.R)
function
in my [R/broman](https://github.com/kbroman/broman) package.

At the start of my R Markdown document, I'd include:

    ```{r load_packages, include=FALSE}
    library(broman)
    ```
    
And then later I could write `` `r myround(cor(x,y), 2)` ``
and it would give `0.90` or `0.00` in the way that I want.