---
layout: post
title: Introducing Clojure
tags: clojure
category: blog
permalink: /blog/introducing-clojure/
author: sachin
comments: true
---


**Clojure** has been around for couple of years now. It has been
recognized for its features like functional programming, elegance,
lisp and JMV support. Unlike many popular dynamic languages, it is
fast and written to take advantages of all optimizations possible with
modern JVMs.

I personally like clojure because it is lisp. Lisp has very tiny
language core with almost no syntax and has a powerful macro support.
With this brief introduction lets start setting up Clojure.

## lein

Before we start programming in Clojure, lets setup
*leiningen*. Leiningen is for automatic Clojure project setup which
will create all necessary file required for any Clojure project.

- Download **lein** binary file from
  [Github](https://raw.github.com/technomancy/leiningen/stable/bin/lein)
  and copy it to your `~/bin/` directory.

        wget <https://raw.github.com/technomancy/leiningen/stable/bin/lein>

- Add `~/bin` PATH in your `~/.bashrc`

        export PATH=~/bin:$PATH

- Make the binary executable

        chmod a+x ~/bin/lein

- Finally run the self installer

        lein

## Lein configuration

- Lein version-2 uses the idea of *profiles*. The location of file is
  `~/.lein/profiles.clj`. Create this file if it does not exist.

- Sample `profiles.clj` file


        {:user {:plugins [[lein-difftest "1.3.8"]
                       [lein-marginalia "0.7.1"]
                       [lein-pprint "1.1.1"]
                       [lein-swank "1.4.5"]
                       [lein-exec "0.3.0"]
                       [lein-ring "0.8.7"]]}}



You can see all the required libraries which are default to all
Clojure projects.

## Upgrade

- To upgrade lein to its latest stable version use,

        lein upgrade

## Project/App

### Create a project or an app.

- Create a project using

        lein new my-project

- Create an app using

        lein new app my-stuff

- Create a noir project(`noir` is a plugin for web framework)

        lein new noir my-web-project

### REPL

REPL(Read-Eval-Print-Loop) can be your excellent interpreter or
debugger while you work on a Clojure project. You can run REPL
once you create a project.

- Lets say the project name is `my-stuff`, go to project directory and
  run REPL using

        cd my-stuff
        lein repl


- Inside `repl` prompt, run `(-main)`

        my-stuff.core=> (-main)


- If you have done some change in a code, reload it

        my-stuff.core=> (require 'my-stuff.core :reload)

- Run a program using `lein` (Outside the REPL prompt.)

        lein run

- If you are happy with your app, package it into an executable `jar`

        lein uberjar

- And run `jar` file using

        java -jar target/my-stuff-0.1.0-standalone.jar

## Library

A Clojure library can be created in a same way.

### Create

    lein new default my-lib


### REPL

    lein repl
    ...

Inside a REPL prompt, simple queries can be performed

    user=> (require 'my-lib.core)
    nil
    user=> (ns my-lib.core)
    nil
    my-lib.core=> (my-func 3)
    9

### Dependencies

- Add project dependencies to `~/.lein/profiles.clj` or
  `your-app/project.clj`

- Below is my sample `profiles.clj` file


        {:user {:plugins [[lein-difftest "1.3.8"]
                         [lein-marginalia "0.7.1"]
                         [lein-pprint "1.1.1"]
                         [lein-swank "1.4.5"]
                         [lein-exec "0.3.0"]
                         [lein-ring "0.8.7"]]}}


- Or you can have it specific to the project

        (defproject perfect-clojure "0.1.0-SNAPSHOT"
         :description "A simple clojure app to test my environment"
         :url "<http://clojuremadesimple.co.uk>"
         :license {:name "Eclipse Public License"
         :url "<http://google.co.uk>"}
         :dependencies
         :dev-dependencies [[midje "1.4.0"]
                            [autodoc "0.9.0"]]
         :plugins
        )

- And setup dependencies using

        lein deps

## Compile

- Compile your project in to an executable `jar` using

        lein uberjar

## Run

- Run the standalone jar using

        java -jar target/my-stuff-0.1.0-SNAPSHOT-standalone.jar

## Connecting to REPL server

- A new REPL server is started at <http://localhost:PORT> when you invoke

        lein repl

  from a project directory.

- You can now connect to existing server using

        lein repl :connect nrepl://localhost:PORT

- for example

        lein repl :connect nrepl://127.0.0.1:37451

## Generate documentation

- Install `marginalia`

        cd ~/.lein
        touch profiles.clj

- Add following line to `profiles.clj` (Your `marginalia` version may
  be different)


        {:user {:plugins }}


- Then, in your project

        cd *path/to/project*

- Install using

        lein deps

- Generate docs

        lein marg

- Browse docs in a web-browser

   *file://path/to/my-proj/docs/uberdoc.html*

## Next (Updated on 03 Feb, 2016)

* Checkout this post on
[Sending an SMS](https://www.twilio.com/blog/2016/02/getting-started-with-clojure.html)
using Clojure.

* [Clojure from the ground up](https://aphyr.com/tags/Clojure-from-the-ground-up)
blog post series by Kyle Kingsbury.

## References

- [http://www.unexpected-vortices.com/clojure/brief-beginners-guide/](http://www.unexpected-vortices.com/clojure/brief-beginners-guide/)
- [http://clojuremadesimple.co.uk/](http://clojuremadesimple.co.uk/)
