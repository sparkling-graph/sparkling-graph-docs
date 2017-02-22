Adamic/Adar
=====================

Adamic/Adar measures is defined as inverted sum of degrees of common neighbours for given two vertices.

:math:`A(x,y)=\sum_{u \in N(x) \cap N(y)}\frac{1}{log(|N(u)|)}`

Where :math:`N(x)` is set of neighbours of vertex :math:`x`

 For further informations please refer to [Adamic]_.


.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val adamicAdarGraph: Graph[_, Double] = graph.adamicAdar(VertexMeasureConfiguration((g:Graph[_,_])=>10l))
	// Graph where each edge is associated with its Adamic/Adar measure


You can also compute closeness centrality for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val adamicAdarGraph: Graph[_, Double] = graph.adamicAdar(treatAsUndirected=true)
	// Graph where each edge is associated with its Adamic/Adar measure  where edges are treated as undirected


References:

.. [Adamic]  Adamic, L. A. and Adar, E. (2003). Predicting missing links via local information.SocialNetworks, 25(3):211–230 `Springer <http://link.springer.com/article/10.1140/epjb/e2009-00335-8>`_
