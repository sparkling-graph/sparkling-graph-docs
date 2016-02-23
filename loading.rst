Loading graph data
===================


Currently library support loading graphs from CSV files only. More formats are planned in future. 


Graph loading API
------------------


Main graph loading object is  a `LoadGraph`_

It takes implementations of a `GraphLoader`_ and lets you easily configure loading process. Parameters (`Parameter`_ ) for configuration are set using ``using(parameter: Parameter)`` method. Parameters are specific for each `GraphLoader`_ 



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


That is simplest way of loading standard CSV file:

.. code-block:: text

	"vertex1","vertex2"
	"<numerical_id_of_vertex_1>","<numerical_id_of_vertex_2>"


In order to change file format you can use parameters like:

.. code-block:: scala

	import ml.sparkling.graph.loaders.csv.GraphFromCsv.LoaderParameters.{Delimiter,Quotation}		
	import ml.sparkling.graph.api.loaders.GraphLoading.LoadGraph
	import ml.sparkling.graph.loaders.csv.GraphFromCsv.CSV
	import org.apache.spark.SparkContext

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value so it will be passed automatically to graph loading API

	val filePath="your_graph_path.csv"
	val graph=LoadGraph.from(CSV(filePath)).using(Delimiter(";")).using(Quotation("'")).load()


Presented snipet will load graph from file with format:

.. code-block:: text

	'vertex1';'vertex2'
	'<numerical_id_of_vertex_1>';'<numerical_id_of_vertex_2>'



### Loading graphs with vertex identifiers that are not numerical


Because in some cases vertices identifiers can be not numerical (username as string). You can load this kind of graph specifying that `Indexing`_ is required:

.. code-block:: scala

	import ml.sparkling.graph.api.loaders.GraphLoading.LoadGraph
	import ml.sparkling.graph.loaders.csv.GraphFromCsv.CSV
	import ml.sparkling.graph.loaders.csv.GraphFromCsv.LoaderParameters.Indexing
	import org.apache.spark.SparkContext

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value so it will be passed automatically to graph loading API

	val filePath="your_graph_path.csv"

	val graph=LoadGraph.from(CSV(filePath)).using(Indexing).load()



That approach gives you ability to load graphs from CSV files with any structure and vertex identifiers of any type. For example:

.. code-block:: text

	"vertex1","vertex2"
	"centralized","computation"
	"is","lame"


Full list of CSV loading parameters is available in `here`_

.. _Indexing: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$LoaderParameters$$Indexing

.. _here: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$LoaderParameters$

.. _GraphLoader: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$GraphLoader

.. _LoadGraph: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$LoadGraph$

.. _Parameter: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$Parameter

.. _CSV implementation: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$CSV$

.. _CSV: https://en.wikipedia.org/wiki/Comma-separated_values




