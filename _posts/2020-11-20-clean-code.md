---
title: clean code
layout: post
categories: code
date:   2020-11-20 21:03:56 +0800
tags: code
excerpt: clean code
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/11/20/clean-code>，转载请申明

------------------
# 目录 <span id="home">
* [code](#1)
	* [code noun](#1.1)
	* [citation needed](#1.2)



----------------------------
# code <span id="1">


## code noun <span id="1.1">

- a set of instructions for a computer
- a computer program,or a portion thereof
- system of words,figures or symbols used to represent others,especially for the purposes of secrecy
- a set of conventions or principles governing behaviour
  or activity in a particular domain
  

why
![why](https://AppleLin8.github.io/assets/img/blog/why_20201120092802.png)


## citation needed  <span id="1.2">

NDC {London}
16-20 January 2017
Inspiring Software Developers
since 2008

short name
![short name](https://AppleLin8.github.io/assets/img/blog/short_name_20201120094900.png)

choose right name
![choose right name](https://AppleLin8.github.io/assets/img/blog/choose_right_name_20201120094945.png)


![bad comment](https://AppleLin8.github.io/assets/img/blog/bad_comment_20201120092447.png)

Clean Coders Hate What Happens to Your Code When You Use These Enterprise Programming Tricks

Refactoring (noun):a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior. oR Kent Bit. Jolin lrnt Refactor(verb): to restructure software by applying a series of refactorings without changing the observable behavior of the software.

Singleton Configuration
Singletons
Verbose Naming
Noisy Logging

Log And Throw

Repetition And Duplication

Unnecessary Code

Mixed Levels Of Abstraction

Legacy Coding Habits

Programming By Coincidence

Programming By Superstition

Kevlin Henney It is all to easy to dismiss problematic codebases on some nebulous idea of bad practice or bad programmers. Poor code, however, is rarely arbitrary and random in its structure or formulation. Systems of code, well or poorly structured, emerge from systems of practice, whether effective or ineffective. To improve code quality, it makes more sense to pick apart the specific practices and see their interplay — the cause — than to simply focus on the code itself — the effect. This talk looks at how a handful of coding habits, design practices and assumptions can systematically balloon code and compound its accidental complexity.  NDC Conferences [https://ndc-london.com](https://www.youtube.com/redirect?q=https%3A%2F%2Fndc-london.com&v=FyCYva9DhsI&event=video_description&redir_token=QUFFLUhqbi1RVkdDT19tWURWQTJualVqTEFSSlZGWGN4QXxBQ3Jtc0ttenI5TUhBMDMzLXRGajYycElaWmw3UEIwSnNwdjJpQW1qT3hjNVhiYTdGeUJET003VG9vZmJRQndKOU1aaVhXdmJnMjducUwyUVNlb2hoMXktcXFBUkJTeXVfX2lPajRDYjNIcExOZURnRWFuNVJSQQ%3D%3D) [https://ndcconferences.com](https://www.youtube.com/redirect?q=https%3A%2F%2Fndcconferences.com&v=FyCYva9DhsI&event=video_description&redir_token=QUFFLUhqbjlxQU92TnpQVHE2SS1kNkRoTWJiUDdyZjhUQXxBQ3Jtc0tsQmRCamE5a0VZaHJTc25WajAwOUxOam1vVm55M2pmejhNM0duX2hQRUFPeDRYSHRVM0l5U2trU0E1cUJXWU4tRThkM1N4ZFQ0N1VWMm85QmVKNjlieFlUNjVHT3pkQlV1dEZ4OWpzZWtsdHAyay1Qbw%3D%3D)NDC {London}
16-20 January 2017
Inspiring Software Developers
since 2008

What if I told you 
Morpheus never says
"What if I told you"?

Cargo cult programming is a style of computer programming characterized by the ritual inclusion of code or program structures that serve no real purpose.
Cargo cult programming can also refer to the results of applying a design pattern or coding style blindly without understanding the reasons behind that design principle.
http://en. wikipedia.org/wiki/Cargo_cult_programming

> I have yet to see any problem, however complicated, which, when you looked at it in the right way, did not become still more complicated.
> Anderson's Law
>
> The default action is executed only if some previous actions were not executed.
> We ask if we can accomplish this without having to check the conditions for the previous actions twice; in other words, if we can make the control flow follow the information flow without loosing modularity.
> MaciejPirog
> "FizzBuzz in Haskell by Embedding a Domain-Specific Language"
>
> A work of art is the unique result of a unique temperament.
> Oscar Wilde
>
> Cargo cult programming is a style of computer programming characterized by the ritual inclusion of code or program structures that serve no real purpose.
> http://en.wikipedia.org/wiki/Cargo_cult programming
>
> 

Signal-to-noise ratio(often abbreviated SNR or S/N) is a measure used in science and engineering that compares the level of a desired signal to the level of background noise.
Signal-to-noise ratio is sometimes used informally to refer to the ratio of useful information to false or irrelevant data in a conversation or exchange.
http/en. awikipedi. org/huiki/Signal_to_noise_ratio

To be,or not to be:that is the question: Whether 'tis nobler in the mind to suffer The slings and arrows of outrageous fortune, Or to take arms against a sea of troubles, And by opposing end them?
William Shakespeare Hamlet

Continuing existence or cessation of existence: those are the scenarios. Is it more empowering mentally to work towards an accommodation of the downsizings and negative outcomes of adversarial circumstance, or would it be agreater enhancement of the bottom line to move forwards to a challenge to our current difficulties, and, by making a commitment to opposition, to effect their demise?
Tom Burton Long Words Bother Me

Comments A delicate matter, requiring taste and judgement.I tend to err on the side ofeliminating comments, for several reasons. First, if the code is clear, and uses good type names and variable names, it should explain itself. Second, comments aren't checked by the compiler, so there is no guarantee they' re right, especially after the code is modified.A misleading comment can be very confusing. Third, the issue of typography: comments clutter code.
Rob Pike,"Notes on Programming in C"

I currently have an average of 15-25 imports in each source file, which is seriously making my code mixed-up and confusing.
Is too many imports in your code a bad thing?
Is there any way around this?

>Avoid Long Import Lists by Using Wildcards Long lists of imports are daunting to the reader.
>We don't want to clutter up the tops of our modules with 80 lines of imports. Rather wewant the imports to be a concise statement about which packages we collaborate with.

It is not a problem.Any IDE will manage imports and show them to you only when needed.
Most IDEs support code folding where all the imports are folded down to one line.I rarely even see my imports these days as the IDE manages them and hides them as well.

Any good IDE, such as Eclipse, will collapse the imports in one line, and you can expand them when needed, so they won't clutter your view.

http://stackoverflow. com/questions/8485689/too-many-imports-spamming-my-code

What is the Matrix?
Control.
The Matrix is a computer-generateddream world built to keep us undercontrol in order to change a human being into this.

A common fallacy is to assume authorsof incomprehensible code will somehowbe able to express themselves lucidly and clearly in comments.
Kevlin Henney https://twitter.com/KevlinHenney/status/381021802941906944

