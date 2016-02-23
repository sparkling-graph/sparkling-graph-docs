Loading graph data
===================


Currently library support loading graphs from CSV files only. More formats are planned in future. 


Graph loading API
------------------


Main graph loading object is  a `LoadGraph`_

It takes implementations of a `GraphLoader`_ and lets you easily configure loading process. Parameters (`Parameter`_ ) for configuration are set using ``using(parameter: Parameter)`` method. PArameters are specific for each `GraphLoader`_ 



Loading from CSV
-----------------

To load graph from `CSV`_ file you must use `CSV implementation`_ of `GraphLoader`_ trait:

.. code-block:: scala

	import ml.sparkling.graph.api.loaders.GraphLoading.LoadGraph
	import ml.sparkling.graph.loaders.csv.GraphFromCsv.CSV
	import org.apache.spark.SparkContext

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value so it will be passed automatically to graph loading API

	val filePath="your_graph_path.csv"

	val graph=LoadGraph.from(CSV(filePath)).load()


 
.. _GraphLoader: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$GraphLoader

.. _LoadGraph: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$LoadGraph$

.. _Parameter: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$Parameter

.. _CSV implementation: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$CSV$

.. _CSV: https://en.wikipedia.org/wiki/Comma-separated_values




