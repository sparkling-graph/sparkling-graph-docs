Eigenvector centrality
=======================

Eigenvector centrality measure give us information about how given node is important in network. It is based on degree centrality. In here we have more sophisticated version, where connections are not equal.

:math:`E(x)=\frac{1}{\lambda}\sum_{j=1}^{n}{A_{ij}x_j}`

Eigenvector centrality is more general approach than PageRank. For further informations please refer to [Newman]_.

Library uses `pregel <http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.graphx.GraphOps@pregel[A](A,Int,EdgeDirection)((VertexId,VD,A)⇒VD,(EdgeTriplet[VD,ED])⇒Iterator[(VertexId,A)],(A,A)⇒A)(ClassTag[A]):Graph[VD,ED]>`_ operator in order to do computations.

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.eigenvectorCentrality()
	// Graph where each vertex is associated with its eigenvector centrality

You can also compute eigenvector centrality for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.eigenvectorCentrality(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is associated with its eigenvector centrality computed for undirected graph

Eigenvector centrality is implemented using iterative approach and Pregel operator. Because of that you can provide your own computation stop predicate:

.. code-block:: scala

	import org.apache.spark.graphx.GraphLoader
	import org.apache.spark.sql.SparkSession
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import ml.sparkling.graph.operators.measures.vertex.eigenvector.EigenvectorCentrality
	import ml.sparkling.graph.operators.OperatorsDSL._

	// initialize your SparkContext as implicit value
	val graph =???
	val eic = EigenvectorCentrality.computeEigenvector(graph,VertexMeasureConfiguration(),(iteration,oldValue,newValue)=>iteration<999).vertices

As you can see, you can also use average values of Eigenvector centrality in consecutive iterations.

References:

.. [Newman]  Newman, M. E. (2008). The mathematics of networks. The new palgrave encyclopedia of economics, 2(2008):1–12., `PDF <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.131.8175&rep=rep1&type=pdf>`_
