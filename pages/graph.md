alias:: Graphs, workspace

- _Graphs_ are the representation of all [[blocks]] and [[pages]] (which are simply blocks) - i.e. all items of knowledge - and their relationship with each other.
- Items (nodes) of a graph can be [[blocks]], [[pages]] and [[tags]] - again, in effect, all of them are the same. The connection between your items of knowledge allows you generate new insights.
- ![image.png](../assets/image_1627833432939_0.png)
- You can think of a graph as your _workspace_ - you can work with different graphs and switch between them, for example to split work and private knowledge (simply click on the graph name on the top right toolbar). In Logseq, each graph is stored as its own folder that includes settings for Logseq and your content.
- **USAGE**
	-
	  1. You can view the graph for a _single_ page: Open the sidebar and select `Page graph`
	  1. You can view the graph for _all_ of your pages: Click on the three dots on the top right and select `View Graph`
-
  #+BEGIN_TIP
  * You can drag individual nodes for easier overview.
  * You can click on individual nodes to open them.
  * The size of the circles represents the number of backlinks.
  * You can search and filter nodes (not for the page graph) - and even combine multiple filters.
  #+END_TIP
-
  #+BEGIN_NOTE
  **Technical details**
  A graph contains content (as files) that is parsed by Logseq to be stored in its database (generated on-the-fly).
  #+END_NOTE
## Using Multiple Graphs
	- You can use as many graphs as you would like. Simply click on the graph menu item in the toolbar and select _Add new graph_.
	- For example, you can use one graph for work and another for personal items.
	-
	  #+BEGIN_TIP
	  You can easily _merge_ graphs as long as there is no overlap in page names. Simply copy the Markdown/Org Mode files from one graph to another. Separating graphs is more challenging as you need to manually select the right files.
	  #+END_TIP
	- **Pro**
		- Separates context
		- Can reuse pages with the same name but different meaning
		- Can easily switch between graphs
		- Improves performance for very large graphs
		- Allows more precise search as out-of-context files are not considered
		- Supports different home pages or themes
	- **Con**
		- You cannot use references across paths
		- Search considers current graph only
		- Switching between graphs returns you to the default home page