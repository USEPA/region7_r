


# Reproducible Research Documents

To do this effectively we need to understand how to create reusable R code and create reproducible reports.  This will be a very high level introduction to both concepts, but should hopefully give you a jumping off place for more learning.

## Lesson Goals
- Understand value of reproducible documents
- Gain familiarity with Markdown, `rmarkdown` and `knitr`
- Create a reproducible document and presentation

## Lesson Outline
- [Introduction to Reproducible Documents](#reproducible-documents)
- [Create a document](#create-a-document)
- [YAML](#yaml)
- [Markdown](#markdown)
- [Code chunks](#code-chunks)
- [Reproducible Presentations](#reproducible-presentations)


## Exercises
- [Exercise 1](#exercise-1)
- [Exercise 2](#exercise-2)


## Reproducible Documents
By itself Markdown is pretty cool, but doesn't really provide any value added to the way most of us already work.  However, when you add in a few other things, it, in my opinion, changes things dramatically.  Two tools in particular that, along with Markdown, have moved reproducible research forward (especially as it relates to R) are, the `knitr` package and a tool called pandoc.  We are not going to cover the details of these, but we will use them via RStudio.  

In short, these three tools allow us to write up documents, embed code via "code chunks", run that code and render the final document with nicely formatted text, results, figures etc into a final format of our choosing.  We can create `.html`, `.docx`, `.pdf`, ...  The benefit of doing this is that all of our data and code are a part of the document.  I share my source document, then anyone can reproduce all of our calculations.  For instance, I can make a manuscript that looks like this:

![Rendered Manuscript](figures/rendered.jpg)

from a source markdown document that looks like:

![Raw RMarkdown](figures/source.jpg)

While we can't get to this level of detail with just the stock RStudio tools, we can still do some pretty cool stuff.  We are not going to do an exercise on this one, but we will walk through an example to create a simple reproducible research document and a presentation using the RStudio interface.  This may seem a departure for me, but anything to increase the adoption of reproducible research is a win!

It should be easy to see how this could be used to write the text describing an analysis, embed the analysis and figure creation directly in the document, and render a final document.  You share the source and rendered document and anyone has access to your full record of that research!

## Create a Document
To create your document, go to File: New File : R Markdown.  You should get a window that looks something like:

![New RMarkdown](/introR/figure/newrmarkdown.jpg)

Add title and author, select "HTML" as the output and click "OK".  RStudio will open a new tab in the editor and in it will be your new document, with some very useful examples.

In this document we can see a couple of things.  In particular we see `YAML`, `Markdown`, and code chunks.

## YAML

    ---
    title: "My First Reproducible Document"
    author: "Jeff W. Hollister"
    date: "1/6/2015"
    output: pdf_document
    ---

This is the YAML(YAML Ain't Markup Language) header or front-matter.  It is metadata about the document that can be very useful.  For our purposes we don't need to know anything more about this.  Below that you see text, code chunks, and if it were included some markdown.  At its core this is all we need for a reproducible document.  We can now take this document, pass it through `knitr::knit()` (remember this syntax from the first lesson?) and pandoc and get our output.  We can do this from the console and/or shell, or we can use RStudio.  


## Markdown
Markdown isn't R, but it has become an important tool in the R ecosystem as it can be used to create package vignettes, can be used on [GitHub](http://github.com), and forms the basis for several reproducible research tools in RStudio.  Markdown is a tool that allows you to write simply formatted text that is converted to HTML/XHTML.  The primary goal of markdown is readibility of the raw file.  Over the last couple of years, Markdown has emerged as a key way to write up reproducible documents, create websites (this whole website was written in Markdown), and make presentations.  For the basics of markdown and general information look at [Daring Fireball](http://daringfireball.net/projects/markdown/basics).

*note: this text borrowed liberally from another class [SciComp2014](http://scicomp2014.edc.uri.edu)*

To get you started, here is some of that same information on the most common markdown you will use in your posts: Text, Headers, Lists, Links, and Images.

### Text

So, for basic text... Just type it!

### Headers

In pure markdown, there are two ways to do headers but for most of what you need, you can use the following for headers:


    # Header 1
    ## Header 2
    ...
    ###### Header 6
  

### List

Lists can be done many ways in markdown. An unordered list is simply done with a `-`, `+`, or `*`.  For example

- this list
- is produced with
- the following 
- markdown.
    - nested

<pre>    
- this list
- is produced with
- the following 
- markdown
    - nested
</pre> 
    
Notice the space after the `-`.  

To create an ordered list, simply use numbers.  So to produce:

1. this list
2. is produced with
3. the following
4. markdown.
    - nested

<pre>
1. this list
2. is produced with
3. the following
4. markdown.
    - nested
</pre>

### Links and Images

Last type of formatting that you will likely want to accomplish with R markdown is including links and images.  While these two might seem dissimilar, I am including them together as their syntax is nearly identical.

So, to create a link you would use the following:

```
[US EPA](https://19january2017snapshot.epa.gov/)
```

Which looks like: [US EPA](https://19january2017snapshot.epa.gov/).

The text you want linked goes in the `[]` and the link itself goes in the `()`.  That's it! Now to show an image, you do this:

```
![EPA Seal](https://www.epa.gov/sites/production/files/2013-06/epa_seal_verysmall_trim.gif)
```

And renders like: ![EPA Seal](https://www.epa.gov/sites/production/files/2013-06/epa_seal_verysmall_trim.gif)

The only difference is the use of the `!` at the beginning.  When parsed, the image itself will be included, and not just linked text.  As these will be on the web, the images need to also be available via the web.  You can link to local files, but will need to use a path relative to the root of the document you are working on.  Let's not worry about that as it is a bit beyond the scope of this tutorial.

And with this, we can have some real fun.  

![matt foley](https://media.giphy.com/media/n7Nwr10hWzROE/giphy.gif)

Now that we can structure out text with Markdown, we need to add the next step: incorportaing code.

## Code Chunks

Since we are talking about markdown and R, our documents will all be R Markdown documents (i.e. .Rmd).  To include R Code in your .Rmd you would do something like:

> 
> ```r
> x<-rnorm(100)
> x
> ```
> 
> ```
> ##   [1]  0.427070457 -0.507814586 -0.444871114 -0.394620222 -2.573294031
> ##   [6] -0.171352356 -1.961924165  0.495670127  0.138570742  0.711322435
> ##  [11]  1.306863588 -0.122966181 -0.375660664 -0.525988486 -0.714000179
> ##  [16] -1.384807855 -0.150874175 -1.103337591  0.989391220  0.724674196
> ##  [21]  0.704521886 -0.436094810  0.779397107  0.439316462 -0.804203309
> ##  [26] -0.122205390 -0.678130128 -1.288041993  0.659831195 -0.392957404
> ##  [31]  0.088637408  1.288966731  0.006475668  1.233512670 -0.471346414
> ##  [36]  0.190134993 -0.314334440 -0.291686338 -0.640859104 -0.876148366
> ##  [41]  0.873539048  0.010118571  0.728987834 -0.693229587 -0.254953986
> ##  [46] -0.181191294 -1.589628638  0.761305449 -0.452220993  1.564559978
> ##  [51] -0.627750896 -0.077498066 -2.392295629 -0.468644721 -0.312795461
> ##  [56] -0.605762531  0.233194945  1.154792810  0.076683644  0.971511325
> ##  [61]  0.388358254  0.020289588 -0.239854723  1.016606968  0.467403745
> ##  [66]  0.591762388  0.427321597 -0.999540841 -0.433219558  0.425056500
> ##  [71]  0.290503148 -0.007158642  0.648486187 -2.334544792 -0.661882877
> ##  [76] -2.059582237 -0.639298838  0.090752280 -0.099964442 -1.735872000
> ##  [81] -0.014261177  1.551259850 -0.265806442  0.424193910 -2.688271978
> ##  [86] -0.698889123 -1.531622701 -0.888200064  0.400364411  0.671624431
> ##  [91] -0.281908092  1.956110043 -2.147438000 -0.461653890  0.388253520
> ##  [96] -1.144198754 -0.326932128  0.007865812 -0.064613648  1.463101612
> ```

This identifies what is known as a code chunk.  When written like it is above, it will echo the code to your final document, evalute the code with R and echo the results to the final document.  There are some cases where you might not want all of this to happen.  You may want just the code returned and not have it evalutated by R.  This is accomplished with:

    ```{r eval=FALSE}
    x<-rnorm(100)
    ```

Alternatively, you might just want the output returned, as would be the case when using R Markdown to produce a figure in a presentation or paper:


    ```{r echo=FALSE}
    x<-rnorm(100)
    y<-jitter(x,1000)
    plot(x,y)
    ```
    
Lastly, each of your code chunks can have a label.  That would be accomplished with something like:
 
    ```{r myFigure, echo=FALSE}
    x<-rnorm(100)
    y<-jitter(x,1000)
    plot(x,y)
    ```

Now, lets do something with the document we have been playing with.

## Rendering

If you look near the top of the editor window you will see:

![knit it](/introR/figure/knit.jpg)

Click this and behold the magic!

## Exercise 1 



## Reproducible Presentations
Creating a presentation is not much different.  We just need a way to specify different slides.

Repeat the steps from above, but this time instead of selecting "Document", select "Presentation".  Only thing we need to know is that a second level header (i.e. `##`) is what specifies the title of the next slide.  Any thing you put after that goes on that slide.  Similar to before, play around with this, add a slide with some new text, new code and knit it.  There you have it, a reproducible presentation.  

I know you will probably wonder can you change the look and feel of this presentation, and the answer is yes.  I have done that, but using a different method for creating slides by using the `xaringan` package.  An example of that presentation is the talk I am giving this afternoon on our [cyanobacteria research efforts](http://jwhollister.com/cyano_open_sci).  It does take a bit more work to set this up and it is admittedly a bit more fiddly than using something like Power Point, but if you have data analysis and results or the talk will need to be updated with new results, then a reproducible presentation begins to make a lot more sense.

Let's take some time and create a new presentation.


## Exercise 2
