# Your Own Continuous Delivery Pipeline

This project should take you through most of the steps for setting up a functional pipeline for your own project. In this project we have a very small product, a tiny webservice implemented in GO - converting integers to their Roman numeral representation.

A pipeline for this small project could contain steps like the following:

 * Build
 * Quick ‘Unit’ test
 * Deploy to a test environment
 * Functional tests
 * Release
 * Deploy to production

When the day is over you should be able to make changes to your Roman numeral implementation and automatically run the build steps all the way to a new release.  This workshop will cover the basics of our CoDe Journey.

 * Test driven development
 * Version control with git
 * Build, test and ship with docker containers
 * Continuous Delivery with Jenkins
 * Implement the praqmatic git flow branching strategy

## Outline of the day

The project will be undertaken in iterations, with each session containing some background teaching, a quick demo, then individual exercise.

The end goal for our development process:

 * A build and test environment with docker for developers
 * Have a jenkins server set up to automatically build `master` branches
 * Automatically delivering successful builds to the production environment
 * Configure the Jenkins jobs using JobDSL and Groovy

Every iteration is divided into the following sections:
   * **Teaching**: explain the concepts we will implement
   * **Demo**: a quick tour of how to implement
   * **Exercise**: your turn to implement

## Slides

 * [CoDe with Containers Slides](http://code.praqma.com/reveals/code-journey/)

## Exercises

  * [Exercise 1 - Your very own fork](journey-exercises/Exercise1.md)
  * [Exercise 2 - Infrastructure as code](journey-exercises/Exercise2.md)
  * [Exercise 3 - First build and test](journey-exercises/Exercise3.md)
  * [Exercise 4 - Jenkins jobs as code](journey-exercises/Exercise4.md)
  * [Exercise 5 - Pre-tested Integration](journey-exercises/Exercise5.md)
  * [Exercise 6 - Extra credit!](journey-exercises/Exercise6.md)


## go-roman - A roman number conversion web service written in go

We need a `go` web service that, when we hit the `/roman/?number=<number>` url, returns the roman numeral representation of it.

````
Given a positive integer number (eg 42) determine
its Roman numeral representation as a String (eg "XLII").

You cannot write numerals like IM for 999.
Wikipedia states "Modern Roman numerals are written by
expressing each digit separately starting with the
leftmost digit and skipping any digit with a value of zero."

Examples:
1 ->    "I" | 10 ->    "X" | 100 ->    "C" | 1000 ->    "M"
2 ->   "II" | 20 ->   "XX" | 200 ->   "CC" | 2000 ->   "MM"
3 ->  "III" | 30 ->  "XXX" | 300 ->  "CCC" | 3000 ->  "MMM"
4 ->   "IV" | 40 ->   "XL" | 400 ->   "CD" | 4000 -> "MMMM"
5 ->    "V" | 50 ->    "L" | 500 ->    "D" |
6 ->   "VI" | 60 ->   "LX" | 600 ->   "DC" |
7 ->  "VII" | 70 ->  "LXX" | 700 ->  "DCC" |
8 -> "VIII" | 80 -> "LXXX" | 800 -> "DCCC" |
9 ->   "IX" | 90 ->   "XC" | 900 ->   "CM" |

1990 -> "MCMXC"  (1000 -> "M"  + 900 -> "CM" + 90 -> "XC")
2008 -> "MMVIII" (2000 -> "MM" + 8 -> "VIII")
  99 -> "XCIX"   (90 -> "XC" + 9 -> "IX")
  47 -> "XLVII"  (40 -> "XL" + 7 -> "VII")

````

Do some work on implementing the Roman Numerals converter, to see the build pipeline in action. Help for the Go-lang syntax can be found here: [Effective GO](https://golang.org/doc/effective_go.html)

Don't focus on using fancy language constructs or using a fancy algorithm. The actual coding exercise is not important - instead focus on the process of making small incremental changes, commiting and pushing them, and see how the Continuous Delivery Pipeline works.
