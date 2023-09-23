> BFS - used to explore and analyze the structure of a graph.

* It opertes in a systematic way, visiting all the vertices of a graph in breadthward motion from a given starting vertex.

```java
/*
* Pseudo code for BFS
* using a queue to keep track of the vertices to be visited.
*/

1. Start with a queue and an empty set to track visited vertices.
2. Enqueue the starting vertex into the queue.
3. Mark the starting vertex as visited.
4. While the queue is not empty:
	* Dequeue a vertex from the queue.
	* Process the vertex
	* Enqueue all unvisited neighboring vertices of the current vertex.
	* Mark each visited neighboring vertex as visited.
5. repeat step 4 until the queue is empty.
```
