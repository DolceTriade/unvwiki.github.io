---
title: Static Analysis
permalink: /Static_Analysis/
---

## What is static analysis?

Static code analysis is a technique to identify potential faults and
vulnerabilities in software without actually running the code. Static
analysis software will examine the code itself to identify possible
problem locations, then work backwards to identify how those could be
reached. John Carmack, founder of id Software, has written an article
[detailing the benefits of the
technique](http://www.altdevblogaday.com/2011/12/24/static-code-analysis/).

## Xcode

To use Xcode 4 to perform static analysis of the code, first follow the
[Xcode compilation
instructions](Compiling_the_source#Mac_OS_X "wikilink"), then in Xcode,
select "Analyze". The process will take considerably longer than just
compiling the source, so be patient.