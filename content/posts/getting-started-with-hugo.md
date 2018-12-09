---
title: "getting started with hugo"
date: 2018-12-09
---

I've been meaning to get going with a technical blog for months, but as it
turned out, 2018 has been quite a busy year: finally finished my PhD, moved
countries, found a new job, a whole mess of personal stuff. In any event, I'm
busy enough now that if I don't start keeping a technical blog it'll be a real
mission to keep on top of what I'm learning. So, blogging it is.

Anyway, I'd had a little flirtation with
the [Jekyll](https://jekyllrb.com/) site generator and [GitHub
Pages](https://pages.github.com/) last year, but between being a novice to
Ruby, someone who last tried making a website around twenty years ago, and
getting caught between some out-of-date documentation, I 
never felt satisfied I was entirely on top of the theme / site generator / repo
set-up. I enjoyed some success around about the time of the World Cup on
a small static project for family, but that was rather simpler, and I had more
time on my hands then.

This time I looked a bit further about, and I ended up getting acquainted with 
with [Hugo](https://gohugo.io/). My curiosity was piqued on learning that it's 
implemented in Go, a language I have slightly more familiarity with, "now draw
the rest of the [expletive deleted] cat" notwithstanding. I figured I could
learn how to use Hugo and take a crack at learning how Hugo actually works at
the same time.  

In the discussion that follows I assume very little knowledge, because that's
where I started from. I do also assume that you're interested in using GitHub
Pages to host your blog, and I haven't explored any other possibilities.

# the big picture 
Hugo generates static websites by parsing and transforming simplified markup
files. The transformed text is injected, along with any asset files (images, PDFs,
etc.), through a set of templates (layouts, themes, etc.) to produce the final
site as a structured directory ready for upload to a mundane webserver. 

So Hugo -- along with other site generators -- more or less resembles LaTeX for
websites.  The motivation is the opportunity to build a static site of non-trivial
size without the hassle and busywork of structuring the project, managing
linkage, and minimizing the extent to which you have to repeat yourself. Your
workflow looks a lot similar, in that you can run Hugo to monitor your source
directory, regenerating and previewing the site locally. If you're managing
your project with Git (why wouldn't you?) you can always push the output to
a public server at major commit / review points. 

A couple of caveats apply, in that the sources are pulled together from more
(content, layout and configuration) files than are typical in a LaTeX workflow,
the output consists of an entire
static directory rather than a single file, and in general, at first, the
process can feel a bit more fragile until it starts to click. 

But [Markdown](https://www.markdowntutorial.com) is nice to work with, and 
makes it nice and easy to commit notes to some kind of temporary record. The
wealth of freely-available themes is a boon for getting something up and
online without committing hours to poring over stylesheets.  

# github (pages) config
I had some early misfires with setup until I chanced upon [whipperstacker's
writeup](http://whipperstacker.com/2015/11/27/deploying-a-stand-alone-hugo-site-to-github-pages-mapped-to-a-custom-domain/),
which I recommend. I'm aiming to try and build on this in my own write-up, as
I found it easy to get confused on a couple of points early on.

On your GitHub account, you'll want to set up two repositories. If you want
to use GitHub Pages to host your site, one of these _has_ to be called
`<username>.github.io`. This will hold the  site _generated_
by Hugo: when you choose to publish updates, this is where the
files will end up.

The second repository holds the files (Markdown, Hugo themes,
image/PDF/MP3/whatever assets) which your site is generated _from_. You can
call this whatever you want.

![Map of repo configuration](githubconfig.png)

The sketch above depicts the setup we're aiming for. On the local
machine, there's a `blog` directory in version control. Within this directory,
there's a `public` subdirectory that contains the static site as (re-)generated
by Hugo. The `public` subdirectory is excluded from its parent directory's
version control. It's placed under version control against the
`<username>.github.io` repository.

Within this setup, the workflow is pretty straightforward. We edit and make
commits in the `blog` directory, and can either preview our changes running
Hugo as a local process, or invoke Hugo to generate a new static site. To
publish to GitHub Pages, we then switch to the `public` subdirectory, commit
changes, and push to remote.  
