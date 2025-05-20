# Pregel example

- https://colab.research.google.com/github/arangodb/interactive_tutorials/blob/master/notebooks/Pregel.ipynb

Pregel was first outlined in a paper published by Google in 2010. It is system for large scale graph processing (think billions of nodes), and has served as inspiration for Apache Giraph, which Facebook uses internally to analyze their social network, as well Apache Spark’s GraphX library, which provides an API for Pregel computations.

A Pregel computation consists of a sequence of iterations, each called a superstep.

> “During a superstep the framework invokes a user-defined function for each vertex, conceptually in parallel. The function specifies behavior at a single vertex V and a single superstep S. It can read messages sent to V in superstep S − 1, send messages to other vertices that will be received at superstep S + 1, and modify the state of V and its outgoing edges. Messages are typically sent along outgoing edges, but a message may be sent to any vertex whose identifier is known.” 

Vertices may choose to halt at a given step, switching its state from activated to deactivated. The Pregel framework will not invoke the function at this vertex from the next superstep onward, unless the vertex is reactivated by a message.

The function can be invoked at each vertex in parallel, since individual vertices communicate via message-passing rather than shared memory.

> “Within each superstep the vertices compute in parallel, each executing the same user-defined function that expresses the logic of a given algorithm. A vertex can modify its state or that of its outgoing edges, receive messages sent to it in the previous superstep, send messages to other vertices (to be received in the next superstep), or even mutate the topology of the graph. Edges are not first-class citizens in this model, having no associated computation.”

The paper also backs the decision to use message-passing rather than shared-memory communication by stating that the researchers had not found any graph algorithms in which message passing was not a sufficient means of communication between vertices.
