Modularity
=====================

Modularity measures strength of division of a network into communities (modules,clusters). Measures takes values from range :math:`<-1,1>`.  Value close to 1 indicates strong community structure. When :math:`Q=0` then the community division is not better than random.

:math:`Q=\sum_{i=1}^{k}{(e_{ii}-a_i^2)}`

Where :math:`k` is number of communities, :math:`e_{ii}`  is number of edges that has both ends in community :math:`i` and :math:`a_i` is number of edges with  one end in community :math:`i`


For further informations please refere to [lecture]_ and [Newman]_. 

.. code-block:: scala
	
	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val modularity: Double= graph.modularity()
	// Modularity value for graph



References: 

.. [lecture]  Carl Kingsford (2009). Modularity, `PDF <https://www.cs.umd.edu/class/fall2009/cmsc858l/lecs/Lec10-modularity.pdf>`_
.. [Newman] Newman, M. E., & Girvan, M. (2004). Finding and evaluating community structure in networks. Physical review E, 69(2), 026113. `PDF <http://arxiv.org/pdf/cond-mat/0308217.pdf>`_