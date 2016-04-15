Community detection
===================

Using library you can easily use state-of-the-art methods for community detection.



SCAN (PSCAN)
------------------

Implementation is based on [Zhao]_. `PSCAN <http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.operators.algorithms.pscan.PSCAN$>`_ bject implements the whole logic of algorithm. Method `computeConnectedComponents(<graph>,<epsilon>)`, takes two parameters:

	* `graph` - on with algorithm will be executed
	* :math:`\epsilon` - used for graph pruning based on similarity measure of edges.

Mentioned similarity is computed as follows:

:math:`sim(v,u)=\frac{|N(v)\cap{} N(u)|}{\sqrt{|N(v)||N(u)|}}`

where :math:`N(v)` is neighbours set of vertex :math:`v` . Edeges with similarity lower than :math:`\epsilon` (:math:`sim(v,u)<\epsilon`) are removed from graph before main part of community detection.

Main part is based on label propagation and is implemented using apropriate `data structures <http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.operators.algorithms.pscan.PSCAN$$PSCANData>`_ and `PREGEL operator <http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.graphx.GraphOps@pregel[A](A,Int,EdgeDirection)((VertexId,VD,A)⇒VD,(EdgeTriplet[VD,ED])⇒Iterator[(VertexId,A)],(A,A)⇒A)(ClassTag[A]):Graph[VD,ED]>`_ 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import ml.sparkling.graph.operators.algorithms.pscan.PSCAN.ComponentID
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val components: Graph[ComponentID, Int] = PSCAN.computeConnectedComponents(graph)
	// Graph where each vertex is asociated with its component identifier


You can also use more readable method using DSL

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import ml.sparkling.graph.operators.algorithms.pscan.PSCAN.ComponentID
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val components: Graph[ComponentID, Int] = graph.PSCAN(epsilon=0.5)
	// Graph where each vertex is asociated with its component identifier


References: 

.. [Zhao] Zhao, W., Martha, V., & Xu, X. (2013, March). PSCAN: a parallel Structural clustering algorithm for big networks in MapReduce. In Advanced Information Networking and Applications (AINA), 2013 IEEE 27th International Conference on (pp. 862-869). IEEE. `PDF <http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6531844&tag=1>`_
