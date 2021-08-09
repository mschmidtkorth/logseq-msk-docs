testproperty:: My value
tags:: myPageTag

- [Documentation](https://logseq.github.io/page/Queries#/page/queries)
- **USAGE**
  section:: Usage
	- You can create simple queries via the `/Query` [[Command]]
	- The syntax for simple queries is `{{query <details>}}`
	- There are important operators:
		- `(not x y ...)`
		- `(and x y ...)`
		- `(or x y ...)`
		- `(between start end)`
			-
			  #+BEGIN_TIP
			  `(between )` can only be used to query for [[Journal]] pages or [[Tasks]].
			  #+END_TIP
			- Possible values: `today, yesterday, tomorrow, now` and relative values `+|-<number> y|m|w|d|h|min`
			- Examples: `(between -7d +7d)` or `(between -2w today)`
- **EXAMPLES**
	- ## General
	  collapsed:: true
		- Limiting the results to those part of the current page
		  query-table:: false
			- You can use a [[macro]] to identify the current page.
			- {{query (and (page <% current page %> block-property section usage))}}
		- Use multiple conditions to search for by separating them via space (_OR_) - only works for text
			-
			  #+BEGIN_NOTE
			  Matching is not an exact match - note how `myTag` also matches `myTagA`. In this query tags are not treated as tags but simply as text.
			  #+END_NOTE
			- {{query myTag my-other-tag}}
			  query-table:: false
			  id:: 610afd9b-ae81-437f-a8c6-ca7830e3e5b3
			  query-properties:: [:block]
			-
			  #+BEGIN_TIP
			  * You could write the same query also with quotation marks - `{{query "myTag" "my-other-tag"}}`
			  * Only wrap tags in `[[]]` if you query for a single tag - otherwise you need to use `(or )`/`(and )` instead of simply separating by space
			  #+END_TIP
		- We can query specifically for "any of the following" tags (via `(or )`):
			- {{query (or [[myTagB]] [[myTagC]])}}
		- We can query for all of the tags (via `(and )`)
		  #+BEGIN_TIP
		  When querying for multiple matches, a check is considered a match also if it is a parent block. For example, `(and [[myTagA]] (todo now))` will _also_ query those blocks where the block's _parents_ have a reference to `myTagA` (and a `NOW` marker).
		  #+END_TIP
			- {{query (and [[myTagB]] [[myTagC]])}}
		- We can exclude certain pages or matches for #myTagC via `(not )`:
		  {{query (and [[myTagA]] [[myTagB]] (not [[myTagC]])) }}
	- ## Pages
	  collapsed:: true
		- Query all pages with name 
		  {{query (page [[properties]])}}
	- ## Tags
	  collapsed:: true
		- Get all blocks with a specific tag `myTag`:
			- {{query [[myTag]] }}
			  query-table:: false
			  query-sort-by:: block
			  query-sort-desc:: false
			- {{query(and [[myTag]]) }}
			- This will return all blocks that are linked to `myTag` - any blocks using `[[myTag]]` or `#myTag`
		- Get all blocks with _any_ tag of the list `myTag, my-other-tag`
			- {{query (or [[myTag]] [[my-other-tag]])}}
		- Get all blocks with _all_ tag of the list `myTagA, myTagB`
			- {{query (and [[myTagA]] [[myTagB]])}}
		- Get all blocks with _all_ tag of the list `myTagA, myTagB` but _not_ `myTagC`
			- {{query (and [[myTagA]] [[myTagB]] (not [[myTagC]])) }}
		- Get all pages with a certain page-level tag (via the special page-property `tags`):
		  {{query (page-tags [[myPageTag]])}}
	- ## Tasks
	  collapsed:: true
		- TODO Task with deadline #sample
		  DEADLINE: <2021-08-07 Sat>
		- We can query tasks via the `todo` keyword (`todo` must always be added as a prefix) - in this example, we limit it to tasks from a specific page via `(and )`:
		  {{query (and (todo todo doing now later done) [[Task Management]])}}
		- Get all tasks that are in status `Now`
			- {{query (todo now)}}
		- Get all tasks that are in status `Done`
			- {{query (todo done)}}
		- Get all tasks with a deadline
			- {{query (todo deadline)}}
			- TODO Not working
		- Get tasks that are on journal entries between certain dates
			- LATER Test
			  SCHEDULED: <2021-08-09 Mon>
			- {{query (and (todo todo later now) (between <% this year %> <% next year %>))}}
			- TODO Make this a fantastic journal entry  #sample
			  SCHEDULED: <2021-08-02 Mon>
			- {{query (and (task later) (between <% this monday %> <% this friday %>))}}
			- {{query (and (todo later) (between <% today %> <% 5 weeks from now %>))}}
	- ## Properties
	  collapsed:: true
		- Query for any block with a property
			- {{query (property testproperty}}
		- Query for any block with a property and specific value
			- {{query (property testproperty "My value")}}
	- ## Files
	  collapsed:: true
		- As any file or images is stored in the `/asset/` folder, you can simply access the [[Asset]] page to see all of your files in the [[Unlinked References]] section