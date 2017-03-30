HITS
===================

After measure computation, each vertex of graph will have assigned two scores ``(hub,authority)``. Where ``hub`` score is proportional to sum of ``authority`` score of its neighbours, and ``authority`` score is proportional to sum of ``hub`` score of its neighbours.

For further informations please refer to [Kleinberg]_. 

Here you can see how to use measure:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[(Double,Double), _] = graph.hits()
	// Graph where each vertex is associated with its hits score (represented as a tuple (auth,hub):(Double,Double))


You can also compute HITS for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.hits(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is associated with its hits score computed for undirected graph


References:

.. [Kleinberg]  Kleinberg, J. M. (1999). Hubs, authorities, and communities. ACM Computing Surveys (CSUR), 31(4es):5.,  `PDF <http://www.csee.umbc.edu/~kolari1/Mining/papers/ft_gateway.cfm.pdf>`_
