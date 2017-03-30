Common Neighbours
=====================

Common Neighbours measure is defined as number of common neighbours of two given vertices.

:math:`CN(x,y)=|N(x)\cap N(y)|`

Where :math:`N(x)` is set of neighbours of vertex :math:`x`

For further informations please refer to [Newman]_.


For memory consumption optimization, informations about neighbours are held in memory efficient implementations of collections available in `fastutil <http://fastutil.di.unimi.it/>`_ library.


.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val commonNeighbours: Graph[_, Int] = graph.commonNeighbours()
	// Graph where each edge is associated with number of common neighbours of vertices on edge


You can also compute common neighbours for graph treated as undirected one:

.. code-block:: scala

	import ml.sparkling.graph.operators.OperatorsDSL._
	import org.apache.spark.SparkContext
	import org.apache.spark.graphx.Graph

	implicit ctx:SparkContext=???
	// initialize your SparkContext as implicit value
	val graph =???
	// load your graph (for example using Graph loading API)

	val commonNeighbours: Graph[_, Int] = graph.commonNeighbours(treatAsUndirected=true)
	// raph where each edge is associated with number of common neighbours of vertices on edge where edges are treated as undirected

References:

.. [Newman]   Newman,  M.  E.  J.  (2001).   Clustering  and  preferential  attachment  in  growing  networks.   pages1–13, `PDF <http://journals.aps.org/pre/pdf/10.1103/PhysRevE.64.025102>`_
