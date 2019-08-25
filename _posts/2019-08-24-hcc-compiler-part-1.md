---
layout: post
title: "hcc - An Incremental Compiler in Haskell"
date: 2019-08-24
---

This is the first post in a series about a tiny C compiler `hcc` (Haskell C Compiler) written in Haskell. A few months ago, I read Abdulaziz Ghuloum's [paper](http://scheme2006.cs.uchicago.edu/11-ghuloum.pdf) on writing an incrmental compiler in Scheme where he implements a small subset of a source language in small steps with the aim of having a "usable" compiler at each step which is capable of compiling small programs. I decided to do this exercise by implmenting a compiler written in Haskell that can compile a "small" subset of C programming language. I debated about using LLVM to generate the backend but decided to instead generate assembly for Intel-x86-64 architecture. This exercise is aimed at learning about compilers, Haskell, assembly and even some corener cases of simple C programs.

All the code is availale on my [hcc repository](https://github.com/karangovil/hcc). I am using [Stack](https://www.haskellstack.org/) for my build system and instructions for building and using `hcc` are listed on the repository. There are [example programs](https://github.com/karangovil/hcc/tree/master/examples) that serve as tests for the compiler in addition to the unit tests.

## Compiler Ingredients

Since we are writing the compiler in Haskell, we will think compositionally and the compiler can be schematically depicted as

``` haskell
compiledResult = generate <$> parse <$> lex source
```

where I have used `<$>` symbol to denote "composition" (however it may be defined for different components). Thus a simple compiler such as `hcc` has the following basic components:

1. Lexer - a component that takes source code as a giant string and parses it to produce a list of tokens based on a set of language rules. 
2. Parser - a component that takes a list of tokens as an input and creates an "Abstract Syntax Tree" (AST) based on the language grammar. 
3. Code generator - a component that takes the AST as an input and translates it into assembly laguage for the target architecture.

At this stage, I should point out that all the above components can be implemented in an imperative language like C or C++ but the functional languages such as Haskell or Ocaml provide powerful abstractions such as algebraic data types with pattern matching that make building and traversing ASTs much easier (note that C++ is a multi paradigm language and many of the functional patterns can be implemented but the syntax is quite clunky and distracts from the logic). Since the aim of this
exercise was to learn about compilers and not build a new super-efficient compiler (which would be likely written in a low level language), I decided to use Haskell as the implementation language.

