title:: Queries/Advanced Queries/Tutorial

-
  #+BEGIN_IMPORTANT
  Playing around with queries can be detrimental to the health of your [[graph]] as you may create blocks and pages just for testing purposes. Use a dedicated playground graph for this!
  #+END_IMPORTANT
- In the following sections you will walk through various examples of querying data in Logseq. The tutorials are intended for beginners getting started with advanced queries in Logseq.
- ## Example 1 - Find a Tag
  id:: 612beaec-f2e0-41eb-902c-924d30050263
	- Let's assume we have a [[tag]] called `MyTag`. We will start with probably the most simple query to just return this page:
		-
		  ```clojure
		  {{query [[MyTag]]}}
		  ```
	- To create it, use the `/query` [[command]] and then add `[[MyTag]]`. This query will look for the tag `#MyTag` anywhere in your [[graph]], you can see it here in all its glory:
		- {{query [[MyTag]]}}
	- The same query written as an [advanced query]([[Queries/Advanced Queries]]) would be:
		-
		  ```clojure
		  #+BEGIN_QUERY
		  {:title "Find tag: MyTag"
		  :query [:find (pull ?b [*])
		              :where
		                [?b :block/ref-pages ?p]
		                [?p :block/name "MyTag"]
		  	       ]
		  }
		  #+END_QUERY
		  ```
	- ### Let's go over this line by line.
		- **\#1** and **\#9** indicate the start and end of a code block. Add them with `<q`, and select _query_ (fun fact: this comes from [[Emacs]] [[org-mode]])
		- **\#2** and **\#8** define our query - a query starts and end with curly brackets
		- **\#2** sets the title via the `title` field - `:title "<some title>"`
		- **\#3** is where the _actual query_ starts. Note the square bracket `[`, opening here, and closing on line **\#7**
		- So, we want to _find_ stuff. The blocks we want to find we store in `?b`. This is just a _variable_ we can use to retrieve these stored blocks, you can replace it with `?qwxlea` if you so please. However, remember to use the same variable anywhere you want to reference it
		- **\#4** `:where` starts the search parameters
		- **\#5** `block/ref-pages` is the reference where _tags_ are stored - that's what we are looking for!
		- **\#6** `block/name` is not the name of the _page_, but of the reference from the previous line **\#5**. We store the name of the tags in `?p` (again this could be anything, you can rename it to `?tagIamLookingFor`)
			- We can write this in a shorter version to be simpler to understand:
			  ```clojure
			  [?b :block/ref-pages [:block/name "MyTag"]]
			  ```
			- This is exactly the same thing, as lines **\#5** and **\#6**. We simply replaced `?p` immediately with `:block/name`.
	- That's all. From now on we will iterate on this, adding complexity.
- ## Example 2 -  Find a Tag That is Also a TODO
	- Let's start with the result:
	-
	  ```clojure
	  #+BEGIN_QUERY
	  {:title "Find: TODO MyTag"
	  :query [:find (pull ?b [*])
	  	:where
	  	[?b :block/marker "TODO"]
	  	[?p :block/name "MyTag"]
	  	[?b :block/ref-pages ?p]]
	  	}
	  #+END_QUERY
	  ```
	- New compared to [Example 1](((612beaec-f2e0-41eb-902c-924d30050263))) is line **\#5**, `:block-marker`. This is where _todo keywords_ are stored (for the curious: [logseq/db_schema](https://github.com/logseq/logseq/blob/master/src/main/frontend/db_schema.cljs), line 57 or so)
	- Our search has to satisfy both line **\#5**, a `marker` containing `TODO`, and **\#6** and **\#7**, which belong together. You can think of all three lines to be connected via an `and` operator.
	-
	  #+BEGIN_QUERY
	  	{:title "Find: TODO MyTag"
	  	:query [:find (pull ?b [*])
	  		:where
	  		[?b :block/marker "TODO"]
	  		[?b :block/ref-pages ?p]
	  		[?p :block/name "mytag"]
	  ]
	  		}
	  	#+END_QUERY
- ## Example 3 - Multiple Markers And TODO States
	-
	  ```clojure
	  #+BEGIN_QUERY
	  {:title "Find: TODO or DOING MyTag"
	  :query [:find (pull ?b [*])
	  :where
	  	[?b :block/marker ?marker]
	  	[(contains? #{"TODO" "DOING"} ?marker)]
	  	[?p :block/name "MyTag"]
	  	[?b :block/ref-pages ?p]]
	  }
	  #+END_QUERY
	  ```
	- Notice lines **\#5** and **\#6**, that replace the single line **\#5** fom the previous example. We're looking for a marker, called `?marker`. We also specify that `?marker` should _contain_ either `TODO` or `DOING`
	-
	  #+BEGIN_QUERY
	  	{:title "Find: TODO or DOING MyTag"
	  	:query [:find (pull ?b [*])
	  	:where
	  
	  	[?b :block/marker ?marker]
	  	[(contains? #{"TODO" "DOING"} ?marker)]
	  
	  	[?p :block/name "mytag"]
	  	[?b :block/ref-pages ?p]]
	  	}
	  	#+END_QUERY
	- You can use the same method to look for multiple tags:
	-
	  ```clojure
	  #+BEGIN_QUERY
	  {:title "Find: MyTag and sample"
	  :query [:find (pull ?b [*])
	  :where
	  
	  	[?b :block/marker ?marker]
	  	[(contains? #{"TODO" "DOING"} ?marker)]
	  
	  	[?b :block/ref-pages ?p]
	  	[?p :block/name ?tag]
	  	[(contains? #{"MyTag" "sample"} ?tag)]]
	  }
	  #+END_QUERY
	  ```
	-
	  #+BEGIN_QUERY
	  	{:title "Find: MyTag and MyOtherTag"
	  	:query [:find (pull ?b [*])
	  	:where
	  
	  		[?b :block/marker ?marker]
	  		[(contains? #{"TODO" "DOING"} ?marker)]
	  
	  		[?b :block/ref-pages ?p]
	  		[?p :block/name ?tag]
	  		[(contains? #{"mytag" "myothertag"} ?tag)]]
	  	}
	  	#+END_QUERY
	-
	  #+BEGIN_IMPORTANT
	  	Notice the closing `]` on line **11**, it's easy to forget these, especially as you slowly add more complexity to your searches
	  	#+END_IMPORTANT
## Example 4 - Search for Parts of a Tag
collapsed:: true
	- Some people have complicated tag configurations, like: `Topic/boats, Topic/airplanes, Topic/automobiles`, to look for _all_ those `Topic`s at the same time, we can use (we, though, stick with our alphabet examples):
	-
	  ```clojure
	  #+BEGIN_QUERY
	  {:query [:find (pull ?b [*])
	  	:where
	  	[?b :block/ref-pages ?p]
	  	[?p :block/name ?tag]
	  	[(clojure.string/starts-with? ?tag "ab")]]
	  }
	  #+END_QUERY
	  ```
	- The key is off course on line **QQ**, where we use `clojure.string/starts-with?`, the variable we work with is `?tag`, and we filter on `ab`, but this could also be something like `Topic/` for those kind of setups
	- For further study, these are the clojure builtins we can use in our queries: [datascript/query.cljc at fork · logseq/datascript](https://github.com/logseq/datascript/blob/fork/src/datascript/query.cljc#L194)
	- Notice also that this query does _not_ have a title, it doesn't _have to_
	-
	  #+BEGIN_QUERY
	  {:query [:find (pull ?b [*])
	  	:where
	  	[?b :block/ref-pages ?p]
	  	[?p :block/name ?tag]
	  	[(clojure.string/starts-with? ?tag "ab")]]
	  }
	  #+END_QUERY
- ## Example 5 -  Search for Page Properties
  collapsed:: true
	- Properties are key-value pairs that allow you to annotate a block or page (see [[Properties]])
	-
	  ```clojure
	  	#+BEGIN_QUERY
	  	{:title "My examples"
	  	:query [:find (pull ?b [*])
	  	:where
	  		[?b :block/properties ?p]
	  		[(get ?p :type) ?t]
	  		[(= "example" ?t)]]}
	  	#+END_QUERY
	  	```
	- There can be multiple `block/properties` to one block, so we have to `get` the one we want, in this case `type`. This can be any word added as a property to a page
	-
	  #+BEGIN_QUERY
	  {:title "My examples"
	  :query [:find (pull ?b [*])
	  :where
	  	[?b :block/properties ?p]
	  	[(get ?p :type) ?t]
	  	[(= "example" ?t)]]}
	  #+END_QUERY
- ## Example 6 - Work With Project Tasks
  collapsed:: true
	-
	  ```clojure
	  	#+BEGIN_QUERY
	  	{:title "My examples TODOs"
	   :query [:find (pull ?b [*])
	       :where
	       [?b :block/marker ?marker]
	       [(contains? #{"NOW" "DOING"} ?marker)]
	  
	  		[?b :block/page ?p]
	  		[?p :block/properties ?a]
	  		[(get ?a :type) ?t]
	  		[(= "example" ?t)]
	       ]
	   :result-transform (fn [result]
	       (sort-by (fn [h]
	           (get h :block/priority "Z")) result))
	   :collapsed? false}
	  	#+END_QUERY
	  	```
	- This query combines the `TODO states` from example 3, and `page properties` from example 5
	- New are lines **13-15**, this snippet will sort TODOs on priority
	-
	  #+BEGIN_QUERY
	  	{:title "My examples TODOs"
	   :query [:find (pull ?b [*])
	       :where
	       [?b :block/marker ?marker]
	       [(contains? #{"NOW" "DOING"} ?marker)]
	  
	  		[?b :block/page ?p]
	  		[?p :block/properties ?a]
	  		[(get ?a :type) ?t]
	  		[(= "example" ?t)]
	       ]
	   :result-transform (fn [result]
	       (sort-by (fn [h]
	           (get h :block/priority "Z")) result))
	   :collapsed? false}
	  	#+END_QUERY
- ## Example 7 - Search Journal Pages for Tagged TODOs
  collapsed:: true
	-
	  ```clojure
	  	#+BEGIN_QUERY
	  	{:title "Tagged journal pages"
	   :query [:find (pull ?b [*])
	  	:where
	  		[?b :block/marker ?marker]
	  		[(contains? #{"TODO" "DOING"} ?marker)]
	  
	  		[?b :block/page ?p]
	  		[?p :block/journal? true]
	  
	  	[?b :block/ref-pages ?r]
	  		[?r :block/name "MyTag"]
	  		]
	   :result-transform (fn [result]
	  			(sort-by (fn [h]
	                                  (get h :block/priority "Z")) result))
	   }
	  	#+END_QUERY
	  	```
	- New are the lines **8** and **9**, where we ask if the page is a `journal`
	-
	  #+BEGIN_QUERY
	  	{:title "Tagged journal pages"
	   :query [:find (pull ?b [*])
	  	:where
	  		[?b :block/marker ?marker]
	  		[(contains? #{"TODO" "DOING"} ?marker)]
	  
	  		[?b :block/page ?p]
	  		[?p :block/journal? true]
	  
	  	[?b :block/ref-pages ?r]
	  		[?r :block/name "MyTag"]
	  		]
	   :result-transform (fn [result]
	  			(sort-by (fn [h]
	  				(get h :block/priority "Z")) result))
	   }
	  	#+END_QUERY
- ## Example 8 - Exclude From a Query
  collapsed:: true
	-
	  ```clojure
	  	#+BEGIN_QUERY
	  	{:title "📼 Watch list - videos"
	  	:query [:find (pull ?b [*])
	  	:where
	  		[?b :block/refs [:block/name "video"]]
	  		(not [?b :block/marker ?marker] [(contains? #{"DONE"} ?marker)])
	  		]
	  	}
	  	#+END_QUERY
	  	```
	- Line **5** searches for the `#video` tag (it's two lines in one, see QQ)
	- Line **6** and **7** look for the `DONE` marker, but now excludes it, by wrapping it in `(not <query>)`. It **has** to be all on one line!
	-
	  #+BEGIN_QUERY
	  	{:title "📼 Watch list - videos"
	  	:query [:find (pull ?b [*])
	  	:where
	  		[?b :block/refs [:block/name "video"]]
	  		(not [?b :block/marker ?marker] [(contains? #{"DONE"} ?marker)])
	  		]
	  	}
	  	#+END_QUERY
- ## Example 9 - Compare Dates
  collapsed:: true
	-
	  ```clojure
	  	#+BEGIN_QUERY
	  	{:title "⚠️ OVERDUE"
	  		:query [:find (pull ?block [*])
	  :in $ ?start ?today
	  :where
	  [?block :block/marker ?marker]
	  
	  (or
	  	[?block :block/scheduled ?d]
	  	[?block :block/deadline ?d])
	  
	  [(>= ?d ?start)]
	  [(<   ?d ?today)]
	  
	  [(contains? #{"NOW" "LATER" "TODO" "DOING" "WAITING"} ?marker)]]
	  	:inputs [:180d :today]
	  	:result-transform  (fn [result]
	  					(sort-by  (fn [d]
	  					(get d :block/deadline) ) result ))
	  	:collapsed? false}
	  	#+END_QUERY
	  	```
	- This is a very useful one. Let's see what it does:
		- Line **6** gets `?marker`, it can (line **15**) contain `NOW, LATER, TODO`, etc
		- Line **8** `or`, means either of these shuold be true, it should _either_ be a `deadline` or `scheduled`
			- `Or` is related to `not` from example 8, there is still a cousin called `and`
		- Lines **12** and **13** are new, you have to read them in the following order:
			- Line **16** offers two values, `:180d` and `:today`
			- Next is line **4**, where those values are assigned to `?start` and `?today` (again, variables, starting with `?` can be called anything, it could have been `?john` and `?ringo`)
			- Finally they are used on lines **12** and **13** where we compare the values of `block/scheduled` (line **9**) to `?start` and `block/deadline` (line **10**) to `?today`
		- And as a bonus, lines **17** to **19**, we sort on deadlines
	-
	  #+BEGIN_QUERY
	  	{:title "⚠ OVERDUE"
	  		:query [:find (pull ?block [*])
	  :in $ ?start ?today
	  :where
	  [?block :block/marker ?marker]
	  (or
	  [?block :block/scheduled ?d]
	  [?block :block/deadline ?d])
	  [(>= ?d ?start)]
	  [(<   ?d ?today)]
	  [(contains? #{"NOW" "LATER" "TODO" "DOING" "WAITING"} ?marker)]]
	  	:inputs [:180d :today]
	  	:result-transform  (fn [result]
	  					(sort-by  (fn [d]
	  					(get d :block/deadline) ) result ))
	  	:collapsed? false}
	  	#+END_QUERY