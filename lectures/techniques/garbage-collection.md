---
layout: page
title: "Garbage Collection"
excerpt: "Garbage Collection"
tags: ["lecture"]
context: lectures
subcontext: techniques
---

## Slides

<iframe src="//www.slideshare.net/slideshow/embed_code/key/J7f2RVCcFoOsyv" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

## Further Reading

1. Andrew W. Appel and Jens Palsberg (2002). Garbage Collection. In *Modern Compiler Implementation in Java*, 2nd edition. Cambridge University Press.
    
    The lecture closely follows the discussion of *mark-and-sweep collection*, *reference counts*, *copying collection*, and *generational collection* in this chapter. This chapter also provides detailed cost analyses and discusses advantages and disadvantages of the different approaches to garbage collection.

2. Oracle. [Java Garbage Collection Basics](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html).
    
    This tutorial covers the basics of how garbage collection works with the Hotspot JVM.
  It explains mark-and-sweep, mark-and-compact, and generational collection.
  It further explains how to monitor the garbage collection process using Visual VM,
  and which garabage collectors are available in the Java SE 7 Hotspot JVM.
  
3. Apple. [Automatic Reference Counting](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html) in [The Swift Programming Language (Swift 3.0.1)](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/index.html#//apple_ref/doc/uid/TP40014097-CH3-ID0)
  
