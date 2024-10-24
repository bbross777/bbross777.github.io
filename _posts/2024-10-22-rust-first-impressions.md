---
layout: post
title: 'first impressions: rust'
category: dev
---

Surprisingly, the first noise I heard relating to Rust was not specifically about the safety features of the language, but rather that it has potential for systems programming. I have been a Linux user for my day-to-day computing for a while now, and work with UNIX OSes at my job, so I was aware that practically everything (in the UNIX sphere) is still written in C and C++. Hearing that such a new language already had enthusiasts in a subfield of programming that some would portray as resistant to change immediately grabbed my attention. So, I decided to see what was compelling about Rust.

After a brief tour of some wikis and documentation, I had gathered that Rust was designed to be fast and, of course, safe. The syntax looked particularly foreign, as it borrows stylistically and philosophically from functional programming languages using the keyword **let** to declare variables, which are immutable unless specified otherwise with **mut**. Already, a different way of thinking of something as fundamental to programming as a variable. This behavior was chosen to ensure that variables cannot be changed unintentionally. At first glance I thought this might be superfluous, but I quickly proved to myself that it is certainly a worthwhile safeguard.

Going deeper, I started writing some programs with the guidance of the official documentation, which was very helpful and did a good job explaining the motivation behind various design choices. "Hello, World" was a breeze as always, and then there were instructions for making a "guess the number" game which explained **Cargo**, Rust's package manager, and how the crate system works. After typing these out and making minor modifications to test out behavior, I moved on to making something of my own. My first small project was a command line game of [Goofspiel](https://en.wikipedia.org/wiki/Goofspiel). This used a random number generator, some nested control flow, and split-out functions to see how complex a small game might be, and I was happy with the results. Once I got used to the way types are handled, I completed the project within a few hours of writing my first "Hello, World!" in the language. I need to spend more time using Cargo to manage dependencies and packages to make a more full judgement, but I can say that having a native package manager for this language with support for marking specific versions of dependencies is very much appreciated.

Next, I wrote a program that would print iterations of a [Rule 90](https://en.wikipedia.org/wiki/Rule_90) cellular automaton to the command line. I chose this because I had recently written the same thing as an exercise for myself in C++, but when I reached the stage where it should have been finished, something was wrong. Somehow, the array of cells was changing in-between being printed in the current iteration, and having the next iteration generated, and I could not for the life of me figure out what was causing it. Printing out the array at each step, doing a lot of manual debugging on each step, checking that I was using all functions properly and safely passing values - for everything I could work out, this program should have printed out Rule 90. I'm sure someone with more patience for debugging something with little to no reward could figure it out, but I had to leave it unsolved at some point and had not felt the need to retry. But, with Rust's penchant for immutable code, I thought this project might end more gracefully, and I am happy to say I was correct! Rewriting the program, I made sure the array of cells was immutable and when passed would not be changed by the process of generating the next iteration. and voila!
```
 █  ███████  █ ██    █ ████  █ █
█ ███     ███  ███  █  █  ███
  █ ██   ██ ████ ███ ██ ███ ██
 █  ███ ███ █  █ █ █ ██ █ █ ███
█ ███ █ █ █  ██      ██     █ ██
  █ █      █████    ████   █  ██
 █   █    ██   ██  ██  ██ █ ████
█ █ █ █  ████ ███████████   █  █
       ███  █ █         ██ █ ██
      ██ ███   █       ███   ███
     ███ █ ██ █ █     ██ ██ ██ █
    ██ █   ██    █   ███ ██ ██
   ███  █ ████  █ █ ██ █ ██ ███
  ██ ███  █  ███    ██   ██ █ ██
 ███ █ ███ ███ ██  ████ ███   ██
██ █   █ █ █ █ █████  █ █ ██ ███
██  █ █        █   ███    ██ █ █
████   █      █ █ ██ ██  ███
█  ██ █ █    █    ██ █████ ██
 ████    █  █ █  ███ █   █ ███
██  ██  █ ██   ███ █  █ █  █ ██
████████  ███ ██ █  ██   ██  ███
```

An unexpected but welcome benefit with the automata project is that the Rust version was *visibly faster*. The C++ version would print line by line (fairly quickly, to be transparent) and I would see the pattern scroll by. The Rust version fills the screen virtually instantly. There is no major change in the algorithm I used between the two, either. Maybe something related to the bug creating the warped version of the automata in the C++ implementation is contributing to slowdown, but I would be surprised to see that program perform at the same level even with that hypothetical issue resolved.

So, after getting this far, I am enjoying Rust. I may have a more nuanced opinion as I delve deeper into other touted features like concurrency and hopefully create a larger-scale project with it. I think some of the syntax is unintuitive, but I think it could be a byproduct of so much time spent in the C++ family. Otherwise, I am looking forward to making something that tests my understanding of structs (which seem fairly compatible with the C/C++ idea of structs) and eventually make something that implements concurrency. 

For the time being, both the Goofspiel program and the automata program are available on my GitHub [here](https://github.com/bbross777/rust-toys) along with any future simple educational programs I make in Rust.

Footnote about the Goofspiel program: the computer opponent is playing cards totally randomly. There is evidence that the best strategy against this is to bid the same value as the value of the prize card :)
