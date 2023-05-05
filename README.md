Download Link: https://assignmentchef.com/product/solved-cse100-lab-11-minimum-spanning-tree
<br>
<h1>Minimum Spanning Tree</h1>

<strong>Description </strong>In the Minimum Spanning Tree problem, we are given as input an undirected graph <em>G </em>= (<em>V,E</em>) together with weight <em>w</em>(<em>u,v</em>) on each edge (<em>u,v</em>) ∈ <em>E</em>. The goal is to find a minimum spanning tree for <em>G</em>. Recall that we learned two algorithms, Kruskal’s and Prim’s in class. In this assignment, you are asked to implement Prim’s algorithm. The following is a pseudo-code of Prim’s algorithm.

Initialize a min-priority queue <em>Q</em>. <strong>for all </strong><em>u </em>∈ <em>V </em><strong>do</strong>

<em>u.key </em>= ∞.

<em>u.π </em>= <em>NIL</em>.

Insert (<em>Q,u</em>).

<strong>end for</strong>

Decrease-key(<em>Q,r,</em>0).

<strong>while </strong><em>Q </em>6= ∅ <strong>do</strong>

<em>u </em>= Extract-Min(<em>Q</em>).

<strong>for all </strong><em>v </em>∈ <em>Adj</em>[<em>u</em>] <strong>do if </strong><em>v </em>∈ <em>Q </em>and <em>w</em>(<em>u,v</em>) <em>&lt; v.key </em><strong>then</strong>

<em>v.π </em>= <em>u</em>.

Decrease-Key(<em>Q,v,w</em>(<em>u,v</em>)).

<strong>end if</strong>

<strong>end for</strong>

<strong>end while</strong>

<strong>Input </strong>The input is <em>G</em>, <em>w</em>, and <em>r</em>, where <em>r </em>is an arbitrary vertex the user can specify as root. The input has the following format. There are two integers on the first line. The first integer represents the number of vertices, |<em>V </em>|. The second integer is the number of edges, |<em>E</em>|. Vertices are indexed by 0<em>,</em>1<em>,…,</em>|<em>V </em>| − 1. Each of the following |<em>E</em>| lines has three integers <em>u,v,w</em>(<em>u,v</em>) representing an edge (<em>u,v</em>) with weight <em>w</em>(<em>u,v</em>). Use vertex 0 as the root <em>r</em>.

<strong>Output </strong>The above pseudo-code stores the MST by <em>π</em>, where <em>v.π </em>= <em>u </em>means that <em>u </em>is <em>v</em>’s unique parent; here, <em>r.π </em>= NIL since <em>r </em>has no parent. Output the MST by outputting the <em>π </em>value of a vertex in each line, in the order 1<em>,</em>2<em>,…,</em>|<em>V </em>| − 1. (Do not output the root’s parent.) <strong>Implementation Issues </strong>Prim’s algorithm requires a min-priority queue that supports the DecreaseKey operation which is not supported by the standard C++ priority queue. You are allowed to use an “inefficient” priority queue that supports each operation in <em>O</em>(|<em>V </em>|) time. Such an inefficient priority queue can be easily implemented using an array. Then, the running time of your implementation is roughly <em>O</em>(|<em>E</em>||<em>V </em>|). However, you may still use the C++ priority queue with a simple “invalidation trick” and have your code to run in <em>O</em>(|<em>E</em>|log|<em>V </em>|). Instead of decreasing an element’s key, just mark the element as invalid and push a new (valid) element with the new key value to the queue. Then you just have to be careful when extracting a minimum element because what you really want is a minimum element that is valid. So extracting a valid min element could take a few iterations. However, at any point in time, the priority queue has at most <em>O</em>(|<em>E</em>|) elements, so each ExtractMin operation takes <em>O</em>(log|<em>E</em>|) = <em>O</em>(log|<em>V </em>|) time. Since you extract minimum elements at most <em>O</em>(|<em>E</em>|) times, you only need <em>O</em>(|<em>E</em>|log|<em>V </em>|) time for extracting valid min elements. To use invalidation trick, you just need to maintain a boolean variable for each vertex to track if it is included in the current MST: when you extract a vertex from the min priority queue, it is valid only if it is not yet part of the current MST.

<strong>Example of input and output</strong>

<em>Input</em>

9

14

0 1 40

<ul>

 <li>7 85</li>

 <li>2 80</li>

 <li>7 110</li>

 <li>3 70</li>

</ul>

2 5 45

<ul>

 <li>8 22</li>

 <li>4 90</li>

 <li>5 140</li>

 <li>5 100</li>

 <li>6 25</li>

 <li>7 10</li>

 <li>8 60</li>

 <li>8 75</li>

</ul>

(The input is a graph with weights given per edge.)

<em>Output</em>

0

1

2

3

2

5

6

2

Here, the first number refers to the parent of vertex 1, and the second number to the parent of vertex 2, and so on. Note that every line is followed by an enter key.

See the lab guidelines for submission/grading, etc., which can be found in Files/Labs.