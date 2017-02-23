Neighborhood Connectivity
==========================

Neighborhood connectivity is a measure based on degree centrality.  Connectivity of a vertex is its degree. Neighborhood connectivity is average connectivity of neighbours of given vertex. 


:math:`NC(x)=\frac{\sum_{k \in N(x)}{|N(k)|}}{|N(x)|}`

Where :math:`N(x)` is set of neighbours of vertex :math:`x`

For further informations please refer to [Maslov]_.


.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.neighborhoodConnectivity()
	// Graph where each vertex is associated with its neighborhood connectivity


You can also compute neighborhood connectivity for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.neighborhoodConnectivity(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is associated with its neighborhood connectivity computed for undirected graph


References:

.. [Maslov] Maslov S, Sneppen K . Specificity and stability in topology of protein networks. Science 2002;296:910-913. `HTML <http://science.sciencemag.org/content/296/5569/910.full>`_
