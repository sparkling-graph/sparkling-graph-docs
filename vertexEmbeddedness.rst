Vertex Embeddedness
=====================

Is an average embededdness of neighbours of given vertex.


:math:`VE(x)=\frac{1}{|N(x)|}\sum_{v \in N(x)}{\frac{|N(x) \cap N(v)|}{|N(x) \cup N(v)|}}`

Where :math:`N(x)` is set of neighbours of vertex :math:`x`

For further informations please refer to [Dong]_.


.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.vertexEmbeddedness()
	// Graph where each vertex is associated with its vertex embeddedness


You can also compute vertex embeddedness for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.vertexEmbeddedness(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is associated with its vertex embeddedness computed for undirected graph

References:

.. [Dong] Dong, Y., Yang, Y., Tang, J., Yang, Y., & Chawla, N. V. (2014, August). Inferring user demographics and social strategies in mobile social networks. In Proceedings of the 20th ACM SIGKDD international conference on Knowledge discovery and data mining (pp. 15-24). ACM. `PDF <https://www3.nd.edu/~nchawla/papers/kdd14b.pdf>`_
