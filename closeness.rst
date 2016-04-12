Closeness centrality
=====================

Closeness centrality measure is defined as inverted sum of distances (``d(y,x)``) from given node to all other nodes. Distance is defined as length of shortest path. 

:math:`C(x)=\frac{1}{\sum_{y \neq x}{d(y,x)}}`

Measure can be understood as how far away from other nodes given node is located. For further informations please refere to [Sabidussi]_. 

Because of computional complexity of shortest paths computation, measure computation can be time consuming. Library uses `pregel <http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.graphx.GraphOps@pregel[A](A,Int,EdgeDirection)((VertexId,VD,A)⇒VD,(EdgeTriplet[VD,ED])⇒Iterator[(VertexId,A)],(A,A)⇒A)(ClassTag[A]):Graph[VD,ED]>`_ operator in order to do computations. 

For memmory consumption optimization, informations about distances are held in memmory efficient implementations of collections available in `fastutil <http://fastutil.di.unimi.it/>`_ library.


.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.closenessCentrality()
	// Graph where each vertex is asociated with its closenss centrality


In order to controll memmory consumption during computation you can use `VertexMeasureConfiguration <http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration>`_ . Just provide appropriate implementation of `BucketSizeProvider <http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.operators.IterativeComputation$>`_ , for example one that will divide computations into buckets of given size (10 in example).

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.closenessCentrality(VertexMeasureConfiguration((g:Graph[_,_])=>10l))
	// Graph where each vertex is asociated with its closenss centrality


You can also compute closeness centrality for graph treating it as undirected one:

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
	// Graph where each vertex is asociated with its closenss centrality computed for undirected graph


.. [Sabidussi]  Sabidussi, G. (1966).  The centrality index of a graph.Psychometrika, 31(4):581–603, `Springer <http://link.springer.com/article/10.1007%2FBF02289527?LI=true>`_