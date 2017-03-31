Partitioning methods
=====================

Library provides multiple methods for graph partitioning. By default GraphX provides only random methods, in SparklingGraph you can find approaches that are using structural properties of graphs in order to minimize computation times and storage overheads. 

All methods can be found in `partitioning package`_


Propagation bases
------------------

In that approach, label propagation is used in order to determine vertex cluster id. In iterative way, alghoritm propagates vertices ids. In each step, vertex selects minimal id from all recived. Steps are repeated until number of components in graph is less than or equal number of requested partitions. If number of unique clusters ids is not equal to the number of requested partitions, alghoritm selects closer solution. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.partitioning.PropagationBasedPartitioning
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph = ???
	// load your graph (for example using Graph loading API)
	val numberOfRequiredPartitions=24
	val partitionedGraph =  PropagationBasedPartitioning.partitionGraphBy(graph,numberOfRequiredPartitions)


Naive PSCAN
------------------

Aglhorimt use PSCAN alghoritm to determine comunities in graph and then use them as partitions. Without configuration, method use default PSCAN configuration, but that can be changed if it is needed. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.partitioning.CommunityBasedPartitioning
	import ml.sparkling.graph.operators.algorithms.community.pscan.PSCAN
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph = ???
	// load your graph (for example using Graph loading API)
	val communityDetectionMethod=PSCAN
	val partitionedGraph =  CommunityBasedPartitioning.partitionGraphBy(graph,communityDetectionMethod)


In order to change parameters you can use

.. code-block:: scala
	
	import ml.sparkling.graph.operators.partitioning.CommunityBasedPartitioning
	import ml.sparkling.graph.operators.algorithms.community.pscan.PSCAN
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph = ???
	// load your graph (for example using Graph loading API)
	val partitionedGraph =  CommunityBasedPartitioning.partitionGraphBy(graph,PSCAN.computeConnectedComponents(_,epsilon = 0))



Dynamic PSCAN
------------------

That is solution that use PSCAN alghoritm in conduction with epsilon parameter search. Aglhoritm looks for possible epsilon values and use binary search to find one that terurns clustering that hase size closest to requested number of partitions. Found clustering is used as partitioning. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.partitioning.PSCANBasedPartitioning
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph = ???
	// load your graph (for example using Graph loading API)
	val numberOfRequiredPartitions=24
	val partitionedGraph =  PSCANBasedPartitioning.partitionGraphBy(graph,numberOfRequiredPartitions)




.. _partitioning package: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.operators.partitioning.package