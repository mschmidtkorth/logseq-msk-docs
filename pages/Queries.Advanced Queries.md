- Advanced queries allow you to specify more detailed, more specific and explicitly formatted queries compared to [[Queries/Simple Queries]].
- ## How to Write Advanced Queries
	- Advanced queries are written via [[Datalog]]
	- Advanced queries can get complex, but their format is always the same:
	  ```
	  {:title  [:strong "<Your query title with optional formatting>"]
	   :query  [:find (pull ?b [*])
	          :where <Your query filter>]
	   :inputs [<Your query input>]
	   :view             (fn [query-result] [:div <Your query result layout>])
	   :result-transform (fn [query-result] <Your query transformation>)
	   :collapsed? true
	   <Your additional query toggles>
	  }
	  ```
	-
	  |Name|Description|Default|Optional|
	  |`title`|Query title, supports [hiccup](((610afd9a-4c78-4099-a333-82dddbddf008))) ||`true`|
	  |`query`|Datascript query||`false`|
	  |`inputs`|Query inputs||`true`|
	  |`view`|`(fn [query-result] <hiccup>)`||`true`|
	  |`result-transform`|`(fn [query-result] <do something>)`||`true`|
	  |`collapsed?`|Whether to collapse the result|`false`|`true`|
	  |`:breadcrumb-show?`|Whether to show the breadcrumb path|`false`|`true`|
	  [Source](https://logseq.github.io/#/page/advanced%20queries)
	-
	  #+BEGIN_TIP
	  You can also write simple queries with advanced query syntax: `{:title "My query" :query (todo todo done)}`
	  #+END_TIP
- ## Query Toggles
	- There are certain properties that allow you to control the output of advanced queries.
	- **USAGE**
		- `:collapsed?` determines whether the query results are collapsed (`true`) or expanded (`false`) by default
		- `:breadcrumb-show?` determines whether to show breadcrumbs in a query result (i.e. the path to the block)
	- **EXAMPLES**
		- This is #myTagA
		-
		  #+BEGIN_QUERY
		  {:title "A collapsed query"
		  :query [:find (pull ?b [*])
		  	       :where
		  	       [?p :block/name "mytaga"]
		  	       [?b :block/ref-pages ?p]]
		  	  :collapsed? true}
		  #+END_QUERY
			-
			  ```clojure
			  #+BEGIN_QUERY
			  {:query [:find (pull ?b [*])
			  	       :where
			  	       [?p :block/name "mytaga"]
			  	       [?b :block/ref-pages ?p]]
			  	  :collapsed? true}
			  #+END_QUERY
			  ```
		-
		  #+BEGIN_QUERY
		  {:title "A query without breadcrumbs"
		  :query [:find (pull ?b [*])
		  	       :where
		  	       [?p :block/name "mytaga"]
		  	       [?b :block/ref-pages ?p]]
		  	  :breadcrumb-show? false}
		  #+END_QUERY
			-
			  ```clojure
			  collapsed:: true
			  #+BEGIN_QUERY
			  {:title "A query without breadcrumbs"
			  :query [:find (pull ?b [*])
			  	       :where
			  	       [?p :block/name "mytaga"]
			  	       [?b :block/ref-pages ?p]]
			  	  :breadcrumb-show? false}
			  #+END_QUERY
			  ```
		-
		  #+BEGIN_QUERY
		  {:title "A query with breadcrumbs"
		  :query [:find (pull ?b [*])
		  	       :where
		  	       [?p :block/name "mytaga"]
		  	       [?b :block/ref-pages ?p]]
		  	  :breadcrumb-show? true}
		  #+END_QUERY
			-
			  ```clojure
			  #+BEGIN_QUERY
			  {:title "A query with breadcrumbs"
			  :query [:find (pull ?b [*])
			  	       :where
			  	       [?p :block/name "mytaga"]
			  	       [?b :block/ref-pages ?p]]
			  	  :breadcrumb-show? true}
			  #+END_QUERY
			  ```
		- ## Formatting Queries
			- TODO Add content
			- ### Query Titles
				- You can name your queries by defining a title. Titles can receive different formatting.
				- **EXAMPLES**
					- Bold text (and plain text)
						-
						  #+BEGIN_QUERY
						  {:title [["All pages that have a "] [:strong "myTagA"] [" tag"]] }
						  #+END_QUERY
						-
						  ```clojure
						  #+BEGIN_QUERY
						  {:title [["All pages that have a "] [:strong "myTagA"] [" tag"]] }
						  #+END_QUERY
						  ```
					- Text styled as a heading
						-
						  #+BEGIN_QUERY
						  {:title [:h3 "My pages"] }
						  #+END_QUERY
						-
						  ```clojure
						  #+BEGIN_QUERY
						  {:title [:h3 "My pages"] }
						  #+END_QUERY
						  ```
		- ## Sorting Results
			- TODO Add content
			- You can use the `sort-by` function to sort results.
		- ## Examples
			- ### Tags
				-
				  #+BEGIN_QUERY
				  query-table:: false
				  {:title "All pages with tag myPageTag"
				   :query [:find (pull ?b [*])
				       :where
				       [?p :page/name "mypagetag"]
				       [?b :block/ref-pages ?p]]
				  :collapsed? true}
				  #+END_QUERY
					-
					  collapsed:: true
					  ```clojure
					  #+BEGIN_QUERY
					  {:title "All pages with tag myPageTag"
					   :query [:find (pull ?b [*])
					       :where
					       [?p :page/name "mypagetag"]
					       [?b :block/ref-pages ?p]]
					  :collapsed? true}
					  #+END_QUERY
					  ```
			- ### Tasks
				- TODO Add content
			- ### Querying [[Hierarchies]]
				- Query all pages part of a hierarchy
				  updated-at:: 1626301594584
				  created-at:: 1626301594584
				  #+BEGIN_QUERY
				  {:title "All pages that start with Home/Gardening"
				   :query [:find (pull ?p [*])
				           :where
				           [?p :block/name ?name]
				           [(str/starts-with (?name) "home/gardening")]
				  ]}
				  #+END_QUERY
					- Alternative
					  updated-at:: 1626301589734
					  created-at:: 1626301588472
						-
						  #+BEGIN_QUERY
						  {:title "Home/Garden child pages"
						   :query [:find (pull ?p [*])
						           :where
						           [?p :block/namespace ?namespace]
						           [?namespace :block/name "home/gardening"]]}
						  #+END_QUERY
						-
						  ```clojure
						  #+BEGIN_QUERY
						  {:title "Home/Garden child pages"
						   :query [:find (pull ?p [*])
						           :where
						           [?p :block/namespace ?namespace]
						           [?namespace :block/name "home/gardening"]]}
						  #+END_QUERY
						  ```
## Resources
	- [Documentation](https://logseq.github.io/page/Queries#/page/advanced%20queries)