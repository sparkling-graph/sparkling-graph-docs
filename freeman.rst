Freeman's network centrality
=============================

Freeman's centrality tells us how heterogenous is degree centrality ammong vertices of network. For start network, we will get a value 1.

:math:`FC(g)=\frac{\sum_{x \in g}{N_{max}-|N(x)|}}{(|g|-1)*(|g|-2)}`

Where :math:`g` is given graph, :math:`N(x)` returns set of neighbours of vertex :math:`x`, :math:`|g|` is number of vertices in graph :math:`g` and :math:`N_{max}` is maximal degree that can be observed in network.

For further informations please refer to [Freeman]_. 

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val freemanCentrality: Double= graph.freemanCentrality()
	// Freeman centrality value for graph



References:

.. [Freeman]  Freeman, L. C. (1978). Centrality in social networks conceptual clarification. Social networks, 1(3), 215-239., `PDF <http://leonidzhukov.ru/hse/2013/socialnetworks/papers/freeman79-centrality.pdf>`_
