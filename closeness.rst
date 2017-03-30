Closeness centrality
=====================

Closeness centrality measure is defined as inverted sum of distances (``d(y,x)``) from given node to all other nodes. Distance is defined as length of shortest path.

:math:`C(x)=\frac{1}{\sum_{y \neq x}{d(y,x)}}`

Measure can be understood as how far away from other nodes given node is located. For further informations please refer to [Sabidussi]_.

Because of computational complexity of shortest paths computation, measure computation can be time consuming. Library uses `pregel <http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.graphx.GraphOps@pregel[A](A,Int,EdgeDirection)((VertexId,VD,A)⇒VD,(EdgeTriplet[VD,ED])⇒Iterator[(VertexId,A)],(A,A)⇒A)(ClassTag[A]):Graph[VD,ED]>`_ operator in order to do computations.

For memory consumption optimization, informations about distances are held in memory efficient implementations of collections available in `fastutil <http://fastutil.di.unimi.it/>`_ library.


.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.closenessCentrality()
	// Graph where each vertex is associated with its closeness centrality


In order to limit memory consumption during computation closeness is computed for each vertex separately. In near future there will be functionality that will let you to decide for how many nodes at once computation should be done.



You can also compute closeness centrality for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.closenessCentrality(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is associated with its closeness centrality computed for undirected graph


References:

.. [Sabidussi]  Sabidussi, G. (1966).  The centrality index of a graph.Psychometrika, 31(4):581–603, `Springer <http://link.springer.com/article/10.1007%2FBF02289527?LI=true>`_
