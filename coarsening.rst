Graph coarsening
=====================

In order to limit computation, you can decrease graph size using coarsening operator. New graph will be smaller because  neighborhood vertices will be coarsed into single vertices. Edges are created using edges from input graph, filtering self loops. 


Label propagation based graph coarsening
-------------------------------------------

One of implementation is based on label propagation. Implementation propagates vertex identifier to neighbours. Neighbours groups them and sorts by number of occurences. If number of occurences is same, minimal one is selected (in order to gurante deterministic execution). Otherwise, vertex identifier with bigest number of occurencies (or minimal one in case of same occurencies number) is selected .

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

