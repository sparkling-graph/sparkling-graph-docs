Eigenvector centrality
=======================

Eigenvector centrality measure give us information about how given node is important in network. It is  based on degree centrality. In here we have more sophisticated version, where connections are not equal. 

:math:`E(x)=\frac{1}{\lambda}\sum{A_{ij}x_j}_{j=1}^{n}`

Eigenvector centrality is more general approach than PageRank. For further informations please refere to [Newman]_. 

Library uses `pregel <http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.graphx.GraphOps@pregel[A](A,Int,EdgeDirection)((VertexId,VD,A)⇒VD,(EdgeTriplet[VD,ED])⇒Iterator[(VertexId,A)],(A,A)⇒A)(ClassTag[A]):Graph[VD,ED]>`_ operator in order to do computations. Computations are done using BSP paradigm. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.eigenvectorCentrality()
	// Graph where each vertex is asociated with its closenss centrality

You can also compute eigenvector centrality for graph treating it as undirected one:

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
	// Graph where each vertex is asociated with its eigenvector centrality computed for undirected graph


.. [Newman]  Newman, M. E. (2008). The mathematics of networks. The new palgrave encyclopedia of economics, 2(2008):1–12., `PDF <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.131.8175&rep=rep1&type=pdf>`_




