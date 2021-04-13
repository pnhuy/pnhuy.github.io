---
layout: post
title: Introduction to Graph Theory
subtitle: Notes from the book Discrete Mathematics with Application (Roshen)
categories: mathematics, discrete mathematics
---

# Graph and Graph models

A graph $G=(V,E)$ consists of $V$, an nonempty set of *vertices* (or *nodes*) and $E$, a set of edges. Each edge has either one or two vertices associated with it, called its *endpoints*. An edge is said to *connect* its endpoints.

A graph with infinite vertex or egdes is called **infinite graph**. In the otherwise case, **finite graph**.

A graph in which each edge connects two different vertices and where no two edges connect the same pair of vertices is called a **simple graph**.

Graph that may have multiple edges connecting the same vertices are called **multigraphs**.

The edges that connect a vertex to itself are called **loops**.

Graphs including loops, and possibly multiple edges connecting the same pair of vertices or a vertex to itself, are called **pseudographs**.

The graph with **undirected** edges is an **undirected graph**.

A directed graph (or digraph) $(V,E)$ consists of a nonempty set of vertices $V$ and a set of directed edges (or arcs) $E$. Each directed edge is associated with an ordered pair of vertices. The directed edge associated with the ordered pair $(u,v)$ is said to start at $u$ and end at $v$.

A directed graph has no loops and has no multiple directed edges is called a **simple directed graph**.

Directed graphs that may have **multiple directed edges** from a vertex to a second (possibly the same) vertex are used to model such networks are called **directed multigraphs**. When there are $m$ directed edges, each associated to an ordered pair of vertices $(u,v)$, we say that $(u,v)$ is an edge of multiplicity $m$.

A graph with both directed and undirected edges is called a **mixed graph**.

Graphs are used in a wide variety of models:
-   Social networks
-   Communication networks
-   Information networks
-   Software design applications
-   Transportation networks
-   Biological networks
-   Tournaments

# Terminology and special types of graph

## Terminology

 Two vertices u and v in an undirected graph G are called **adjacent** (or **neighbors**) in G if u and v are endpoints of an edge e of G. Such an edge e is called **incident with** the vertices u and v and e is said to connect u and v.

The set of all neighbors of a vertex v of $G=(V,E)$, denoted by $N(v)$, is called the **neighborhood** of $v$. If $A$ is a subset of $V$ , we denote by $N(A)$ the set of all vertices in $G$ that are adjacent to at least one vertex in A. So, $N(A)=\bigcup_{v\in A}N(v)$.

The **degree of a vertex in an undirected graph** is the number of edges incident with it, *except that a loop at a vertex contributes twice to the degree of that vertex*. The degree of the vertex v is denoted by $deg(v)$.

A vertex of degree zero is called **isolated** (not adjacent to any vertex).

A vertex is **pendant** if and only if it has degree one (adjacent to exactly one other vertex).

> Theorem
> The handshaking theorem
> Let $G=(V,E)$ be an undirected graph with $m$ edges:
> 
> $$2m=\sum_{v\in V}\deg(v)$$

This theorem shows that the sum of the degrees of the vertices of an undirected graph is even, which lead to the below theorem.

> Theorem:
> An undirected graph has an even number of vertices of odd degree.

When $(u,v)$ is an edge of the graph G with directed edges, $u$ is said to be **adjacent to** $v$ and $v$ is said to be **adjacent from** $u$. The vertex $u$ is called the **initial vertex** of $(u,v)$, and $v$ is called the **terminal** or **end vertex** of $(u,v)$. The initial vertex and terminal vertex of a loop are the same.

In a graph with directed edges the **in-degree** of a vertex v, denoted by $\deg^{-}(v)$, is the number of edges with v as their terminal vertex. The **out-degree** of v, denoted by $\deg^{+}(v)$, is the number of edges with v as their initial vertex. (Note that a loop at a vertex contributes 1 to both the in-degree and the out-degree of this vertex.)

> **Theorem** 
> 
> Let $G=(V,E)$be a graph with directed edges:
> 
> *$$\sum_{v\in V}\deg^{-}(v)=\sum_{v\in V}\deg^{+}(v)=|E|$$*

Some special simple graphs:
-   Complete Graphs: a complete graph on n vertices, denoted by $K_{n}$, is a simple graph that contains exactly one edge between each pair of distinct vertices.
-   Wheels
-   n-cube / n-dimensional hypercube, denoted by $Q_{n}$, is a graph that has vertices representing the $2^{n}$ bit strings of length n.

## Bipartite Graph

A simple graph $G$ is called **bipartite** if its vertex set $V$ can be partitioned into two disjoint sets $V_{1}$ and $V_{2}$ such that every edge in the graph connects a vertex in $V_{1}$ and a vertex in $V_{2}$ (so that no edge in $G$ connects either two vertices in $V_{1}$ or two vertices in $V_{2}$). When this condition holds, we call the pair $(V_{1},V_{2})$ a bipartition of the vertex set $V$ of $G$.

> **Theorem** 
> 
> A simple graph is bipartite if and only if it is possible to assign one of two different colors to each vertex of the graph so that no two adjacent vertices are assigned the same color.

A **complete bipartite graph** $K_{m,n}$ is a graph that has its vertex set partitioned into two subsets of $m$ and $n$ vertices, respectively with an edge between two vertices if and only if one vertex is in the first subset and the other vertex is in the second subset.

A **matching** $M$ in a simple graph $G=(V,E)$ is a subset of the set $E$ of edges of the graph such that no two edges are incident with the same vertex. In other words, a matching is a subset of edges such that if ${s,t}$ and ${u,v}$ are distinct edges of the matching, then s, t, u, and v are distinct.

A vertex that is the endpoint of an edge of a matching $M$ is said to be matched in $M$; otherwise it is said to be unmatched.

A **maximum matching** is a matching with the largest number of edges. We say that a matching M in a bipartite graph $G=(V,E)$ with bipartition $(V_{1},V_{2})$ is a complete matching from $V_{1}$ to $V_{2}$ if every vertex in $V_{1}$ is the endpoint of an edge in the matching, or equivalently, if $\|M\|=\|V1\|$.

> **Theorem**
> Necessary and sufficient conditions for complete matching (Hall's marriage theorem)
> The bipartite graph $G=(V,E)$ with bipartition $(V_{1},V_{2})$ has a complete matching from $V_{1}$ to $V_{2}$ if and only if $|N(A)|\ge|A|$ for all subsets A of $V_{1}$.
