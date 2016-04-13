Local Clustering Coefficient
=============================

Local Clustering Coefficient for vertex tells us howe close its neighbors are. It is number of exsisting connections in neghboorhod divided by number of all possible connections. 

:math:`LC(x)=\sum_{v \in N(x)}{\frac{|N(x) \cap N(v)|}{|N(x)|*(|N(x)|-1)}}`

Where ``N(x)`` is set of neighbours of vertex ``x``

For further informations please refere to [Watts]_. 


.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.localClustering()
	// Graph where each vertex is asociated with its local clustering coefficient



You can also compute local clustering coefficient for graph treating it as undirected one:

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.localClustering(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is asociated with its local clustering coefficient computed for undirected graph

References: 

.. [Watts] D. J. Watts and Steven Strogatz, “Collective dynamics of ‘small-world’ networks”, Nature, vol. 393, pp 440-442, 1998 `HTML <http://www.nature.com/nature/journal/v393/n6684/full/393440a0.html>`_




