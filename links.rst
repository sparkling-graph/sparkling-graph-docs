Link Prediction
===================

Using library you can easily use state-of-the-art methods for link prediction.


Measure based link prediction
------------------

Basic appraoch that is using simmilarity computed between two vertices. `MeasureBasedLnkPredictor`<http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.operators.algorithms.link.MeasureBasedLnkPredictor>_ is trait for that approach


Basic measure based link prediction
+++++++++++++++++++++++++++++++++++++

Most basic implementation of measure based link prediction. All possible vertices combinations are computed for given graph. In next step, similarity measure is computed for each combination. Combinations that exsits or creates loops (self connections) are filtered out. Combinations that have similarity lower than given treshold are also filtered out. Implementation can be found in `BasicLinkPredictor <http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.operators.algorithms.link.BasicLinkPredictor$>`_

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.operators.measures.edge.CommonNeighbours
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val predictedEdges: RDD[(VertexId,VertexId)] = graph.predictLinks(edgeMeasure=CommonNeighbours,threshold=10)
	// RDD with predicted edges using Common Neighbours measure, and 10 as a minimal number of common neighbours

You can also predict links for graph treated as undirected one:

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.operators.measures.edge.AdamicAdar
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val predictedEdges: RDD[(VertexId,VertexId)] = graph.predictLinks(edgeMeasure=AdamicAdar,threshold=2,treatAsUndirected=true)
	// RDD with predicted edges using Adamic/Adar measure, and 2 as a minimal value of measure, graph is treated as undirected



