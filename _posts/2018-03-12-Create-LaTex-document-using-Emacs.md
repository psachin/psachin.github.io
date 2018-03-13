


This post is inspired by the post titled [A introduction to creating
documents in
LaTeX](https://opensource.com/article/17/6/introduction-latex) by
[Aaron Cocker](https://opensource.com/users/aaroncocker) where he
introduces how to create first LaTeX document. He also introduced few
LaTeX editors which users find good for creating LaTeX documents.

What drew my attention was the first comment to the post by [Greg
Pittman](https://opensource.com/users/greg-p) where is says "_LaTeX
seems like an awful lot of typing when you first start..._". In a way
this is true. For beginners, LaTeX is a lot if typing and debugging(if
you missed to escape a special character like an exclamation mark!)
which is enough for a beginner to start searching for a replacement.
So in this post let me introduce you to GNU Emacs to create LaTeX
documents.

## Create your first document.

Lets start with configuring Emacs. I promise this to be quick and
easy. Copy below snippet to a file `latex.el` and save to a path where
you can find it easily. I suggest you save it in home
directory as ``~/latex.el``.

```
;;; Add LaTeX beamer sections/subsections
(require 'ox-latex)
(add-to-list 'org-latex-classes
             '("beamer"
               "\\documentclass\[presentation\]\{beamer\}"
               ("\\section\{%s\}" . "\\section*\{%s\}")
               ("\\subsection\{%s\}" . "\\subsection*\{%s\}")
               ("\\subsubsection\{%s\}" . "\\subsubsection*\{%s\}")))

;;; Minted
(setq org-latex-listings 'minted)

;;; Minted options
(setq-default org-export-latex-minted-options
              '(("frame" "lines")
                ("fontsize" "\\scriptsize")
                ("linenos" "")))

;;; Custom language environment.
(setq-default org-export-latex-custom-lang-environments
              '((emacs-lisp "common-lispcode")
                (cc "c++")
                (cperl "perl")
                (shell-script "bash")
                (caml "ocaml")
                (ruby "ruby")
                (python "python")))

;;; Run shell process when 'M-x org-beamer-export-to-pdf' is called.
(setq org-latex-pdf-process
      '("pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f"
        "pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f"
        "pdflatex -shell-escape -interaction nonstopmode -output-directory %o %f"))
```

Once done, start Emacs using below command
```
emacs -q --load ~/latex.el
```
For those who are curious,
`-q` will not load any other Emacs initialization(if present) and `--load`
will only load `~/latex.el` file, our LaTeX specific customization.
This should pop-up Emacs as shown in image below.


[IMAGE: emacs_startup.png]
(Caption: GNU Emacs startup screen)

Now go to "File" in menu-bar on top and select **Visit New File**. Name
new file as `helloworld.org`.

[IMAGE: create_new_file.png]
(Caption: Creating a new file in Emacs)

Its time to put some LaTeX headers. We do this the Emacs way. Go to
"Org" in menu-bar and select "Export/Publish".

[IMAGE: insert_template_flow.png]
(Caption: Insert default template)

In next window, Emacs give options to either export or insert a
template. We insert the template by entering **#**([#] Insert
template). It will as move cursor to mini-buffer where the prompt says
**Options category:**. At this time you may know the category name. A
TAB will show possible completion. Type "default" and press Enter.
Following content will be inserted.


```
#+TITLE: helloworld
#+DATE: <2018-03-12 Mon>
#+AUTHOR:
#+EMAIL: makerpm@nubia
#+OPTIONS: ':nil *:t -:t ::t <:t H:3 \n:nil ^:t arch:headline
#+OPTIONS: author:t c:nil creator:comment d:(not "LOGBOOK") date:t
#+OPTIONS: e:t email:nil f:t inline:t num:t p:nil pri:nil stat:t
#+OPTIONS: tags:t tasks:t tex:t timestamp:t toc:t todo:t |:t
#+CREATOR: Emacs 25.3.1 (Org mode 8.2.10)
#+DESCRIPTION:
#+EXCLUDE_TAGS: noexport
#+KEYWORDS:
#+LANGUAGE: en
#+SELECT_TAGS: export
```


Change the title, date, author and email as you wish. Mine looks like
below.
```
#+TITLE: Hello World! My first LaTeX document
#+DATE: \today
#+AUTHOR: Sachin Patil
#+EMAIL: psachin@redhat.com
```

I don't want table of content to be created for now hence I change value of
`toc` from `t` to `nil` in line below.
```
#+OPTIONS: tags:t tasks:t tex:t timestamp:t toc:nil todo:t |:t
```

Its time for a section and paragraphs. A section starts with an
asterisk(*). Lets copy content of paragraphs from Aaron's post,
```
* Introduction

  \paragraph{}
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras lorem
  nisi, tincidunt tempus sem nec, elementum feugiat ipsum. Nulla in
  diam libero. Nunc tristique ex a nibh egestas sollicitudin.

  \paragraph{}
  Mauris efficitur vitae ex id egestas. Vestibulum ligula felis,
  pulvinar a posuere id, luctus vitae leo. Sed ac imperdiet orci, non
  elementum leo. Nullam molestie congue placerat. Phasellus tempor et
  libero maximus commodo.
```

With content in place its time to export the content as PDF. Select
**Export/Publish** from **Org** menu again but this time type
**l**(**[l] Export to LaTeX**) and then **o**(**[o] As PDF file and
open**). This not only opens PDF file for you to view but also save
file as `helloworld.pdf` in the same path as `helloworld.org`.


[IMAGE: org_tex_pdf.png]
(Caption: Emacs with LaTeX, org and PDF file opened in three windows)

You can also export to PDF by pressing `Alt + x` followed by typing
"org-latex-export-to-pdf". Use TAB to auto-complete.

Guess what's more? Emacs also creates `helloworld.tex` file for you to
have fine control. You can compile `.tex` file to `.pdf` using the
command,
```
pdflatex helloworld.tex
```

The `.org` file as more to offer. It can be exported to HTML or as
simple text file. What I like about org files is they can be pushed to
[GitHub](https://github.com) where they are rendered just like any
other markdown formats.


## Create LaTeX Beamer presentation

Let go a step ahead and see how to create a LaTeX beamer presentation
using the same file with some modifications as below. Create a new
file with the name `presentation.org`
```
#+TITLE: LaTeX Beamer presentation
#+DATE: \today
#+AUTHOR: Sachin Patil
#+EMAIL: psachin@redhat.com
#+OPTIONS: ':nil *:t -:t ::t <:t H:3 \n:nil ^:t arch:headline
#+OPTIONS: author:t c:nil creator:comment d:(not "LOGBOOK") date:t
#+OPTIONS: e:t email:nil f:t inline:t num:t p:nil pri:nil stat:t
#+OPTIONS: tags:t tasks:t tex:t timestamp:t toc:nil todo:t |:t
#+CREATOR: Emacs 25.3.1 (Org mode 8.2.10)
#+DESCRIPTION:
#+EXCLUDE_TAGS: noexport
#+KEYWORDS:
#+LANGUAGE: en
#+SELECT_TAGS: export
%% Those three lines are added for beamer
#+LATEX_CLASS: beamer
#+BEAMER_THEME: Frankfurt
#+BEAMER_INNER_THEME: rounded


* Introduction
*** Programming
    - Python
    - Ruby

*** Paragraph one

    Lorem ipsum dolor sit amet, consectetur adipiscing
    elit. Cras lorem nisi, tincidunt tempus sem nec, elementum feugiat
    ipsum. Nulla in diam libero. Nunc tristique ex a nibh egestas
    sollicitudin.

*** Paragraph two

    Mauris efficitur vitae ex id egestas. Vestibulum
    ligula felis, pulvinar a posuere id, luctus vitae leo. Sed ac
    imperdiet orci, non elementum leo. Nullam molestie congue
    placerat. Phasellus tempor et libero maximus commodo.

* Thanks
*** Links
    - Link one
    - Link two
```

To export to PDF press `Alt + x` followed by typing
"org-beamer-export-to-pdf".

[IMAGE: LaTeX_Beamer_presentation.png]
(Caption: Latex Beamer presentation created using Emacs and Org mode.)

Emacs Org mode offers lot more than we covered in this post. Please
refer
[orgmode.org](https://orgmode.org/worg/org-tutorials/org-latex-export.html)
to learn more.
