---
layout: page
title: "Milestone 3: Code Generation"
excerpt: "Milestone 3: Code Generation"
tags: ["assignment"]
context: assign
subcontext: ms3
---

{% include _toc.html %}

In this milestone, you extend the MiniJava editor from the previous milestone to a MiniJava compiler, which is able to generate Java class files from MiniJava programs.

## Jasmin Editor

Jasmin is an assembler for the Java Virtual Machine.
It takes ASCII descriptions of Java classes, written in a simple assembler-like syntax using the Java Virtual Machine instruction set.
It converts them into binary Java class files, suitable for loading by a Java runtime system.
Basically, Jasmin is a nice syntax for Java bytecode, with a compiler to actual Java bytecode in class files.

### Usage

We provide you with a Jasmin editor which was built with Spoofax.
You can edit Jasmin files with a Spoofax editor.
The editor's menu entries allow you to inspect the abstract syntax of Jasmin files, to generate Java class files from them, and to execute those class files.
Your initial project will contain several Jasmin example programs which you should explore in order to get used to Jasmin's syntax.

## Material

We consider the following material to be useful for this milestone.

1. Lecture on Virtual Machines

    In [this lecture](/lectures/techniques/virtual-machines), we discussed the architecture of the JVM, some Java bytecode instructions, and different approaches to code generation in Spoofax.

2. Java Virtual Machine Specification

    Oracle provides an [online version][JVM] of the Java Virtual Machine Specification.
    [Chapter 3][JVMch3] and [Chapter 6][JVMch6] are particularly helpful for this milestone.
    Furthermore, you can find a comprehensive list of [Java Bytecode instructions][JBCInstructions] in the English Wikipedia.

[JVM]: http://docs.oracle.com/javase/specs/jvms/se8/html/
[JVMch3]: http://docs.oracle.com/javase/specs/jvms/se8/html/jvms-3.html
[JVMch6]: http://docs.oracle.com/javase/specs/jvms/se8/html/jvms-3.html
[JBCInstructions]: https://en.wikipedia.org/wiki/Java_bytecode_instruction_listings

3. Stratego documentation

    The Stratego language is described in the [Stratego language manual](http://hydra.nixos.org/job/strategoxt-docs/strategoxt-manual/html/latest/download/1/manual/chunk-chapter/stratego-language.html).
    Useful strategies in the Stratego standard library are described with examples in [Stratego library manual](http://hydra.nixos.org/job/strategoxt-docs/strategoxt-manual/html/latest/download/1/manual/chunk-chapter/stratego-library.html).
    A complete listing of all strategies in the Stratego standard library can be found in the [API documentation](http://releases.strategoxt.org/docs/api/libstratego-lib/stable/docs/).
