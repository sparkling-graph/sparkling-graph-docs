Graph coarsening
=====================

In order to limit computation, you can decrease graph size using coarsening operator. New graph will be smaller because  neighborhood vertices will be coarsed into single vertices. Edges are created using edges from input vertices, filtering self loops. 


Label propagation based graph coarsening
-------------------------------------------

One of implementation is based on label propagation. Just three iterations are enaught in order to coarse graph. Implementation propagates vertex identifier to neighbours. Neighbours groups them and sorts by number of occurences. If number of occurences is same, greater one is selected (in order to gurante deterministic execution). After that last id is selected (one with bigest number of occurences, or greatest one). After three iterations, vertices has their final IDs.

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import ml.sparkling.graph.api.operators.algorithms.coarsening.CoarseningAlgorithm.Component
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val coarsedGraph: Graph[Component, _] = graph.LPCoarse()
	// Graph where each vertex has new ID and is associated vertex IDs from input graph that where coarsed and forms together new vertex 


You can also coarse graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import ml.sparkling.graph.api.operators.algorithms.coarsening.CoarseningAlgorithm.Component
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val coarsedGraph: Graph[Component, _] = graph.LPCoarse(treatAsUndirected=true)
	// Graph coarsed treating input graph as undirected

