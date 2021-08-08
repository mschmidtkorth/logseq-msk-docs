tags:: myPageTag
section:: Usage

- Queries are used to _ask questions_ to your knowledge content. You can query for [[pages]], [[blocks]], [[tags]], [[tasks]] and more.
- There are two types of queries: [[Queries/Simple Queries]] and [[Queries/Advanced Queries]] .
-
  #+BEGIN_TIP
  **Debugging queries**
  Whenever your queries do not seem to return the right result, you can debug them and check for syntax errors - open the _Developer Tools_ in your browser, go to the _Console_ tab and look for `$APP.Tl` (click on it)
  ![image.png](../assets/image_1625748582353_0.png){:height 280, :width 464}
  #+END_TIP
-
  #+BEGIN_TIP
  **Querying page names or properties**
  When querying for page names or properties always write them in _lowercase_ - this is how they are stored in Logseq's database
  #+END_TIP
-
  #+BEGIN_TIP
  **Queries as tables & sorting**
  * You can render query results as tables (click on the toggle) and select which fields/columns to include.
  * You can sort table by clicking on a column name.
  #+END_TIP
-
  #+BEGIN_NOTE
  **Technical details**
  Queries are written in the [[Datalog]] progamming language ([Wikipedia](https://en.wikipedia.org/wiki/Datalog)).  There are various flavours/systems of Datalog. A common one is _DataScript_, written in Clojure, the programming language Logseq is written in (or rather ClojureScript). DataScript is an in-memory database running on either ClojureScript or Java (JVM). Another common one is _Datomic_, which is a commercial database.
  #+END_NOTE
## Queries in [[Journal]] Pages
	- You can add default queries to each new journal entry (displayed at the bottom) by editing the [[config.edn]] file in your [[Graph]] directory and adding them to this section:
	  id:: 610afd9a-36b6-475b-bdaa-e03c64ca3c0c
	  ```clojure
	  :default-queries
	  {:journals
	    [
	  ;; Your queries here:
	  ;; {query1}
	  ;; {query2}
	    ]
	  }
	  ```
		-
		  #+BEGIN_WARNING
		  Many default queries may slow down Logseq (see [here](((6109951e-1c4d-4491-8147-9c4072672d56)))).
		  #+END_WARNING
## Query Table Functions
id:: 610fdfba-d6cf-4bb1-a88d-b3fe28e0a72d
	- You can use _functions_ to process a query table's output.
	- Functions allow you to perform aggregations such as calculating the sum or average value (`sum`, `average`, minimum (`min`), maximum (`max`), `total`) or by performing an arbitrary function written in Clojure.
		- Aggregations always have the format of `{{function (<aggregation type> :<property keyword>)}}`
	- **USAGE**
		-
		  1. Create a query in table view
		  1. Define a function in this query's child block
	- **EXAMPLES**
		- Let's create a few block properties.
		  type:: query-table-block
		  name:: my-first-block
		  index:: 1
		  number-of-sentences:: 1
		- And here is another block.
			- This block is also going to have block properties.
			  type:: query-table-block
			  name:: my-second-block
			  index:: 2
			  number-of-sentences:: 2
		- And lastly, a third block.
			- Similar to the other two blocks, we are going to add some properties.
			- This block is also going to have a new property.
			- This is going to be the last block.
			  type:: query-table-block
			  name:: my-third-block
			  index:: 3
			  number-of-sentences:: 4
			  is-last-block:: true
		- {{query (property type query-table-block)}}
		  query-table:: true
		  query-properties:: [:name :index :number-of-sentences :is-last-block]
			- Now, let's calculate
				- the average number of sentences: {{function (average :number-of-sentences)}} (`{{function (average :number-of-sentences)}}`)
				- the highest number of sentences: {{function (max :number-of-sentences)}} (`{{function (max :number-of-sentences)}}`)
				- the number of all sentences: {{function (sum :number-of-sentences)}} (`{{function (total :number-of-sentences)}}`)
				- something arbitrary like multiplying the index of each block with its number of sentences (like a weighting), and taking the sum of all: {{function (sum (map (fn [x] (* (:index x) (:number-of-sentences x))) result))}} `{{function (sum (map (fn [x] (* (:index x) (:number-of-sentences x))) result))}}`
			-
			  #+BEGIN_WARNING
			  The function has to be a child of the query table.
			  #+END_WARNING
## Resources
	- TODO Check
	- [Domain Modeling with Datalog](https://www.youtube.com/watch?v=oo-7mN9WXTw&t=1s) (Norbert Wojtowicz)
	- [Learn Datalog Today](http://www.learndatalogtoday.org/)
	- [Datascript 101](https://udayv.com/blog/2016-04-28-datascript101/)
- TODO ==Anything below is work in progress!==
- Advanced queries
	- Query all tasks part of a specific group from your journal entries
	-
	  #+BEGIN_QUERY
	  query-table:: false
	  {:title "All pages that have a myPageTag tag"
	   :query [:find ?name
	         :in $ ?tag
	         :where
	         [?t :block/name ?tag]
	         [?p :page/tags ?t]
	         [?p :block/name ?name]]
	   :inputs ["mypagetag"]
	   :view (fn [result]
	         [:div.flex.flex-col
	          (for [page result]
	            [:a {:href (str "/page/" page)} (clojure.string/capitalize page)])])}
	  #+END_QUERY
		-
		  #+BEGIN_NOTE
		  This query returns manually generated links - the navigation will be different than what you are used to in Logseq (not recommended for Desktop app).
		  #+END_NOTE
	-
	  #+BEGIN_QUERY
	  {:title "All page tags"
	  :query [:find ?tag-name
	          :where
	          [?tag :tag/name ?tag-name]]
	  :view (fn [tags]
	          [:div#query-all-page-tags
	           (for [tag (flatten tags)]
	             [:a.tag.mr-1 {:href (str "/page/" tag)}
	              (str "#" tag)])])}
	  #+END_QUERY
- (not sure if true)`:block/name` is the block's name; note that there is [no `:page/name`](https://github.com/logseq/logseq/blob/master/src/main/frontend/db_schema.cljs) - a page is simply a special block -> no, there is
	-
	  created-at:: 1626300859256
	  updated-at:: 1626300859256
	  #+BEGIN_QUERY
	  {:query [:find (pull ?b [*])
	       :where
	       [?p :block/name "myTagA"]
	       [?b :block/ref-pages ?p]]
	  :collapsed? true}
	  #+END_QUERY
	- <page_name> <keyword 1>, without <keyword 2> OR ["page" "keyword" "not this keyword"]
	  #+BEGIN_QUERY
	  {:query [:find (pull ?b [*])
	           :in $ ?pagename ?keyword ?not
	           :where
	           [(str "(?i)" ?keyword) ?matcher1]
	           [(re-pattern ?matcher1) ?regex1]
	           [(str "(?i)" ?not) ?matcher2]
	           [(re-pattern ?matcher2) ?regex2]
	           [?p :block/original-name ?pagename]
	           [?b :block/page ?p]
	           [?b :block/content ?c]
	           (not [(re-find ?regex2 ?c)])
	           [(re-find ?regex1 ?c)]]
	   :inputs ["page" "keyword" "not this keyword"]
	   }
	  #+END_QUERY
	- Sort by priority
	  #+BEGIN_QUERY
	        {:title "🟢 ACTIVE"
	          :query [:find (pull ?h [*])
	                  :in $ ?start ?today
	                  :where
	                  [?h :block/marker ?marker]
	                  [?h :block/page ?p]
	                  [?p :page/journal? true]
	                  [?p :page/journal-day ?d]
	                  [(>= ?d ?start)]
	                  [(<= ?d ?today)]
	                  [(contains? #{"NOW" "DOING"} ?marker)]]
	          :inputs [:14d :today]
	          :result-transform (fn [result]
	                              (sort-by (fn [h]
	                                         (get h :block/priority "Z")) result))
	          :collapsed? false}
	  #+END_QUERY
	- Add links
	  ```clojure
	  (let [nickname (second (:url (second (first title))))]
	                           [:a {:href (str "page/" nickname)}
	                            nickname])
	  ```
	- Querying tasks
		-
		  #+BEGIN_QUERY
		  {:title "🔨 NOW"
		      :query         [:find (pull ?h [*])
		                         :in $ ?start ?today
		                         :where
		                         [?h :block/marker ?marker]
		                         [(contains? #{"TODO "NOW" "DOING"} ?marker)]
		                         [?h :block/page ?p]
		                         [?p :block/journal? true]
		                         [?p :block/journal-day ?d]
		                         [(>= ?d ?start)]
		                         [(<= ?d ?today)]]
		      :inputs        [:14d :today]
		      :result-transform (fn [result]
		                          (sort-by (fn [h]
		                                         (get h :block/priority "Z")) result))
		      :collapsed? false}
		  #+END_QUERY
		-
		  ```clojure
		  {:title            "🔨 NOW"
		      :query            [:find (pull ?h [*])
		                         :in $ ?start ?today
		                         :where
		                         [?h :block/marker ?marker]
		                         [(contains? #{"NOW" "DOING"} ?marker)]
		                         [?h :block/page ?p]
		                         [?p :block/journal? true]
		                         [?p :block/journal-day ?d]
		                         [(>= ?d ?start)]
		                         [(<= ?d ?today)]]
		      :inputs           [:14d :today]
		      :result-transform (fn [result]
		                          (sort-by (fn [h]
		                                     (get h :block/priority "Z")) result))
		      :collapsed?       false}

		  {:title      "📅 NEXT"
		      :query      [:find (pull ?h [*])
		                   :in $ ?start ?next
		                   :where
		                   [?h :block/marker ?marker]
		                   [(contains? #{"NOW" "LATER" "TODO"} ?marker)]
		                   [?h :block/ref-pages ?p]
		                   [?p :block/journal? true]
		                   [?p :block/journal-day ?d]
		                   [(> ?d ?start)]
		                   [(< ?d ?next)]]
		      :inputs     [:today :7d-after]
		      :collapsed? false}
		  ```
	- Not working - limited to current page ... https://discuss.logseq.com/t/query-todos-on-current-page/1481 https://discord.com/channels/725182569297215569/743670484863811649/816094510223589396
		- LATER Test
		  SCHEDULED: <2021-08-01 Sun>
		  DEADLINE: <2021-08-02 Mon>
		- {{query (todo later)}}
		- {{query (and (todo todo later now) (between today tomorrow))}}
		- {{query (and (todo todo later now) (between <% today %> <% tomorrow %>))}}
		- {{query (and (task later) (between <% this monday %> <% this friday %>))}}
		- {{query (and (todo later) (between <% today %> <% 5 weeks from now %>))}}
		- {{query (and ([[mine]]) (page-property parent <% current page %>))}}
		- {{query (page-property parent <% current page %>)}}
		  query-table:: false
		- {{query (page-property parent <% current page %>)}}