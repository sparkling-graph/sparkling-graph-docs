Degree centrality
===================

Degree of a node is number of connections that its has. When we have directed network, we can distinguish indegree (input edges) and outdegree (output edges). 
We can treate degree as a centrality measure. Nodes with high degree can be assumed as important. Ofcourse it depends on the sitution, and interpretations can differ. 

For further informations please refere to [lecture]_. 

Method returns a tuple ``(outdegree,indegree):(Int,Int)``. If computations will be done using ``treatAsUndirected``, both values will be equal. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[(Int,Int), _] = graph.degreeCentrality()
	// Graph where each vertex is asociated with its degree centrality in form of tuple (outdegree,indegree):(Int,Int)



You can also compute closeness centrality for graph treated it as undirected one:

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import ml.sparkling.graph.api.operators.measures.VertexMeasureConfiguration
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val centralityGraph: Graph[Double, _] = graph.degreeCentrality(VertexMeasureConfiguration(treatAsUndirected=true))
	// Graph where each vertex is asociated with its degree centrality computed for undirected graph in form of tuple (degree,degree):(Int,Int)


References: 

.. [lecture]  Dr. Cecilia Mascolo,  Social and Technological Network'Analysis `PDF <https://www.cl.cam.ac.uk/teaching/1213/L109/stna-lecture3.pdf>`_