Graph generators
===================

Using library you can easily generate networks using commonly used models.


Ring
------------------

Generator creates simple ring network with given number of node.

.. code-block:: scala
	
	import ml.sparkling.graph.generators.ring.{RingGenerator, RingGeneratorConfiguration}
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	
	val graph =RingGenerator.generate(RingGeneratorConfiguration(numberOfNodes=5))
	
	// do operations on graph


Network can be also created in undirected version:

.. code-block:: scala
	
	import ml.sparkling.graph.generators.ring.{RingGenerator, RingGeneratorConfiguration}
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	
	val graph =RingGenerator.generate(RingGeneratorConfiguration(numberOfNodes=5,undirected = true))
	
	// do operations on graph



Watts And Strogatz
------------------


Model accepts three parameters:

	* n - number of nodes
	* k - mean degree
	* :math:`\beta` - probability of rewiring

Generation is done in two steps:

	#. Ring network with :math:`n` nodes is created, each of nodes is connected to :math:`\frac{k}{2}` nodes on left and right 
	#. Each edge is rewired with probability :math:`\beta`, where new destination node is seleted randomly from all possible not exsisting connections


For further informations please refere to  [Watts]_

.. code-block:: scala
	
	import ml.sparkling.graph.generators.wattsandstrogatz.{WattsAndStrogatzGenerator, WattsAndStrogatzGeneratorConfiguration}
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	
	val graph =WattsAndStrogatzGenerator.generate(WattsAndStrogatzGeneratorConfiguration(numberOfNodes = 10,meanDegree = 2,rewiringProbability = 0.5))
	
	// do operations on graph



References:

.. [Watts] Watts, D. J., & Strogatz, S. H. (1998). Collective dynamics of ‘small-world’networks. nature, 393(6684), 440-442. `Nature <http://www.nature.com/nature/journal/v393/n6684/full/393440a0.html>`_

