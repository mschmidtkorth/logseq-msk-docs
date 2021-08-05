- Queries are used to _ask questions_ to your knowledge content. You can query for [[pages]], [[blocks]], [[tags]], [[tasks]] and more.
- There are two types of queries: [[Queries/Simple Queries]] and [[Queries/Advanced Queries]] .
-
  #+BEGIN_TIP
  Whenever your queries do not seem to return the right result, you can debug them and check for syntax errors - open the _Developer Tools_ in your browser, go to the _Console_ tab and look for `$APP.Tl` (click on it)
  ![image.png](../assets/image_1625748582353_0.png){:height 280, :width 464}
  #+END_TIP
-
- Technical details
	- Queries are written in the _[Datalog](https://en.wikipedia.org/wiki/Datalog)_ progamming language.  There are various flavours/systems of Datalog. A common one is _DataScript_, written in Clojure, the programming language Logseq is written in (or rather ClojureScript). DataScript is an in-memory database running on either ClojureScript or Java (JVM). Another common one is _Datomic_, which is a commercial database.
## Resources
	- [Domain Modeling with Datalog](https://www.youtube.com/watch?v=oo-7mN9WXTw&t=1s) (Norbert Wojtowicz)
	- [Learn Datalog Today](http://www.learndatalogtoday.org/)
	- [Datascript 101](https://udayv.com/blog/2016-04-28-datascript101/)
- TODO ==Anything below is work in progress!==
- ## Queries in [[Journal]] Pages
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
		  Many default queries may slow down Logseq. (see [here](((6109951e-1c4d-4491-8147-9c4072672d56))))
		  #+END_WARNING
- Advanced queries
	-
	  #+BEGIN_TIP
	  **Querying page names**
	  When querying for page names always write them in _lowercase_ - this is how they are stored in Logseq's database.
	  #+END_TIP
	- ### How to Write Queries
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
	  #+BEGIN_QUERY 
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
	-
	  #+BEGIN_QUERY
	  {:title "All pages with tag myPageTag"
	   :query [:find (pull ?b [*])
	       :where
	       [?p :page/name "mypagetag"]
	       [?b :block/ref-pages ?p]]
	  :collapsed? true}
	  #+END_QUERY
	-
	  ```clojure
	  #+BEGIN_QUERY
	  {:title "All pages with tag myTagA"
	   :query [:find (pull ?b [*])
	       :where
	       [?p :page/name "mytaga"]
	       [?b :block/ref-pages ?p]]
	  :collapsed? true}
	  #+END_QUERY
	  ```
	- ?p = short for ?page, ?b = short for ?block but imo random names
	- (not sure if true)`:block/name` is the block's name; note that there is [no `:page/name`](https://github.com/logseq/logseq/blob/master/src/main/frontend/db_schema.cljs) - a page is simply a special block
	-
	  created-at:: 1626300859256
	  updated-at:: 1626300859256
	  #+BEGIN_QUERY
	  {:query [:find (pull ?b [*])
	       :where
	       [?p :block/name "praise"]
	       [?b :block/ref-pages ?p]]
	  :collapsed? true}
	  #+END_QUERY
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
		  SCHEDULED: <2021-08-01 Sun>
		- {{query (todo later)}}
		- {{query (and (todo todo later now) (between today tomorrow))}}
		- {{query (and (todo todo later now) (between <% today %> <% tomorrow %>))}}
		- {{query (and (task later) (between <% this monday %> <% this friday %>))}}
		- {{query (and (todo later) (between <% today %> <% 5 weeks from now %>))}}
		- {{query (and ([[mine]]) (page-property parent <% current page %>))}}
		- {{query (page-property parent <% current page %>)}}
		  query-table:: false
		- {{query (page-property parent <% current page %>)}}