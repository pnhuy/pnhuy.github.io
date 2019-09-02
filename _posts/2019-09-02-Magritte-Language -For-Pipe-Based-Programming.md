---
layout: post
title: Magritte -- A Language for Pipe-Based Programming
categories: reading, programming
---

## Abstract

This work proposes **Magritte**, a general-purpose language that is viable as a shellscripting language. Like shells, it manages concurrent processes which are composedby connecting implicit input and output streams with a pipe. Unlike traditional byte-stream-based pipes, however, **Magritte** pipes can process rich values, enabling their use as a more general composition mechanism, which enables Magritte to express concurrent processes as normal functions.

Included in the design are modern language features such as data structures and lambda functions with lexical scope, as well as systems for automatic process cleanup and error handling. The syntax is also designed to optimize for command-line usability.

This work also presents an implementation, along with a proposed method of integration with a POSIX system.

Thesis: http://files.jneen.net/academic/thesis.pdf