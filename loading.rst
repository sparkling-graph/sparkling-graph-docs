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




Loading graphs with vertex identifiers that are not numerical
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++



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


Loading from GraphML
--------------------
To load graph from `GraphML`_ XML file you must use `GraphML implementation`_ of `GraphLoader`_ trait:

.. code-block:: scala

	import ml.sparkling.graph.api.loaders.GraphLoading.LoadGraph
	import ml.sparkling.graph.loaders.graphml.GraphFromGraphML.GraphML
	import org.apache.spark.SparkContext

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value so it will be passed automatically to graph loading API

	val filePath="your_graph_path.xml"

	val graph=LoadGraph.from(GraphML(filePath)).load()

That is simplest way of loading standard `GraphML`_  XML file (vertices are automatically indexed, and receive ``VertexId`` identifier ):

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8"?>
	<graphml xmlns="http://graphml.graphdrawing.org/xmlns"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://graphml.graphdrawing.org/xmlns/1.0/graphml.xsd">
	    <key id="v_name" for="node" attr.name="name" attr.type="string"/>
	    <key id="v_type" for="node" attr.name="type" attr.type="string"/>
	    <graph id="G" edgedefault="undirected">
	        <node id="n0">
	            <data key="v_name">name0</data>
	            <data key="v_type">type0</data>
	        </node>
	        <node id="n1">
	            <data key="v_name">name1</data>
	        </node>
	        <node id="n2">
	            <data key="v_name">name2</data>
	        </node>
	        <node id="n3">
	            <data key="v_name">name3</data>
	        </node>
	        <edge id="e1" source="n0" target="n1"/>
	        <edge id="e2" source="n1" target="n2"/>
	    </graph>
	</graphml>

All attributes associated with vertices will be puted into `GraphProperties`_ type which expands to ``Map[String,Any]``. By default each edge and vertex has ``id`` attribute.

.. code-block:: scala

	import ml.sparkling.graph.api.loaders.GraphLoading.LoadGraph
	import ml.sparkling.graph.loaders.graphml.GraphFromGraphML.{GraphProperties, GraphML}
	import org.apache.spark.SparkContext

	implicit ctx:SparkContext=??? 
	// initialize your SparkContext as implicit value so it will be passed automatically to graph loading API

	val filePath="your_graph_path.xml"

	val graph: Graph[GraphProperties, GraphProperties] =LoadGraph.from(GraphML(filePath)).load()
	val verticesIdsFromFile: Array[String] = graph.vertices.map(_._2("id").asInstanceOf[String]).collect() 



.. _Indexing: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$LoaderParameters$$Indexing$

.. _here: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$LoaderParameters$

.. _GraphLoader: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$GraphLoader

.. _LoadGraph: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$LoadGraph$

.. _Parameter: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.api.loaders.GraphLoading$$Parameter

.. _CSV implementation: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.csv.GraphFromCsv$$CSV$

.. _GraphML implementation: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.graphml.GraphFromGraphML$$GraphML$

.. _CSV: https://en.wikipedia.org/wiki/Comma-separated_values

.. _GraphML: http://graphml.graphdrawing.org/

.. _GraphProperties: http://sparkling-graph.github.io/sparkling-graph/latest/api/#ml.sparkling.graph.loaders.graphml.GraphFromGraphML$




