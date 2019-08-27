---
layout: post
title: "STL Algorithms"
date: 2019-08-26"
---

C++ STL or the Standard Template Library is one of the most important tools in a C++ programmer's arsenal. The [STL proposal](http://stepanovpapers.com/STL/DOC.PDF) by Alexander Stepanov and Meg Lee is dated October 31, 1995 and became an important part of the first ISO C++ standard or C++98 as it is referred to nowadays. David Musser and Alexander Stepanov had already written about [Generic Programming](http://stepanovpapers.com/genprog.pdf) in Ada and STL was developed along similar
ideas. Given the popularity of object oriented (OO) paradigm in the 90s, it is a bit surprising that STL (which was implemented in the 90s) is not OO at all and is based on generic programming with smaller components that are meant to be composed and used with templates for compile-time polymorphism rather than the typical run-time polymorphism common with OO paradigm. However, this is in line with the idea that C++ is supposed to be used as a multi-paradigm language. Anyone who says that OO or
functional or generic programming is a silver bullet and will solve all the problems has just not seen enough problems. This flexibility of C++ is one of the key reasons that makes it such a popular language (backward compatibility being the other).

STL is often criticized for not being fast enough (game developers often roll out their own STL like functionality) or having some subtle issues in the implementation, but it is still a great model of thinking about data structures and algorithms. Understanding the implementations of STL algorithms and data structures is essential for an informed programmer, even if she needs to roll out a bespoke implementation.

In this post I will go over the basic taxonomy of STL algorithms and in subsequent posts go over the implementation details, complexity analysis, and examples of each algorithm. Nicolai Josuttis' [The C++ Standard Library](https://www.amazon.com/Standard-Library-Tutorial-Reference-2nd/dp/0321623215/ref=sr_1_1?crid=2W7YX4L42GRXG&keywords=nicolai+josuttis&qid=1566873181&s=gateway&sprefix=nicolai+jos%2Caps%2C144&sr=8-1) is one of the best resources for someone starting out with STL.

The STL algorithms operate on STL containers which provide an interface for the algorithms to operate on data without knowing the exact implementation of the data structure. This is done with iterators (and ranges in future) along with function predicates (lambdas and function objects). A large majority of the algorithms are found in the `algorithm` header but some algorithms are provided for numeric procession and found in the `numeric` header. Jonathan Boccara of
[fluentcpp](http://www.fluentcpp.com) has a very nice illustration of all STL algorithms in the form of a [map](http://www.fluentcpp.com/getTheMap/). Josuttis provides the following classification
* Non-mutating algos - these do not mutate the data structures and only query the data through input and forward iterators. Examples include `search()`, `is_sorted()`, `count_if()` etc.
* Mutating algos - as the name suggests, these mutate the data either in place or as they are being copied to another ddata structure. Examples include `transform()`, `for_each()`, `generate()` etc.
* Remover algos - these are a subset of mutating algorithsm that filter or remove data based on a predicate. Examples include `remove()`, `unique()` etc.
* Sorting algos - STL provides a variety of sorting algos for various time critical applications. Examples include `sort()`, `partition()`, `nth_element()` etc.
* Numeric algos - these are used with data that "behaves" numerically (for e.g. strings can be concatenated with `+` operation). Examples include `accumulate()`, `inner_product` etc.

There isn't a universal taxonomy of STL algos but most fall under the categories above (or combinations thereof). In future posts, we will start looking at these algorithms in more detail with a view towards implementation and space-time complexity.
