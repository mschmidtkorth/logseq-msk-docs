testproperty:: My value
tags:: myPageTag

- [Documentation](https://logseq.github.io/page/Queries#/page/queries)
- **USAGE**
  section:: Usage
	- You can create simple queries via the `/Query` [[Command]]
	- The syntax for simple queries is `{{query <details>}}`
- **EXAMPLES**
	- ## General
		- There are important operators:
			- `(not x y ...)`
			- `(and x y ...)`
			- `(or x y ...)`
			- `(between start end)`
				-
				  #+BEGIN_TIP
				  `(between )` can only be used to query for [[Journal]] pages.
				  #+END_TIP
				- Possible values: `today, yesterday, tomorrow, now` ad relative values `+|-<number> y|m|w|d|h|min`
				- Examples: `(between -7d +7d)` or `(between -2w today)`
		- Limit the results to those part of the current page
		  query-table:: false
		  {{query (and (page <% current page %> block-property section Usage))}}
		- Use multiple conditions to search for by separating them via space (_OR_) - only works for text
			-
			  #+BEGIN_NOTE
			  Matching is not an exact match - note how `myTag` also matches `myTagA`. In this query tags are not treated as tags but simply as text.
			  #+END_NOTE
			- {{query myTag my-other-tag}}
			  query-table:: true
			  id:: 610afd9b-ae81-437f-a8c6-ca7830e3e5b3
			  query-properties:: [:block]
		-
		  #+BEGIN_TIP
		  * You could write the same query also with quotation marks - `{{query "myTag" "my-other-tag"}}`
		  * Only wrap tags in `[[]]` if you query for a single tag - otherwise you need to use `(or )`/`(and )` instead of simply separating by space
		  #+END_TIP
		- We can also query specifically for tags:
			- {{query (or [[myTagB]] [[myTagC]])}}
			- {{query (and [[myTagB]] [[myTagC]])}}
		- Or we can query for any other type such as todos - in this example, we limit it to todos from a specific page via `(and )`:
		  {{query (and (todo now later done) [[queries]])}}
		- We can exclude certain pages or matches for #myTagC via `(not )`:
		  {{query (and [[myTagC]] (not [[some page]] [[another page]]))}}
		-
	- ## Tags
		- Get all blocks with a specific tag `myTag`:
			- {{query [[myTag]] }}
			  query-table:: false
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
		- Get all todos that are in status `Now` (`todo` must be added as a prefix)
			- {{query (todo now)}}
		- Get all todos that are in status `Done`
			- {{query (todo done)}}
		- Get all todos with a deadline
			- {{query (todo deadline)}}
			- {{query (deadline)}}
			- TODO How to limit only to task, not where text matches?
	- ## Properties
		- Query for any block with a property
			- {{query (property testproperty}}
		- Query for any block with a property and specific value
			- {{query (property testproperty "My value")}}
	- ## Files
		- As any file or images is stored in the `/asset/` folder, you can simply access the [[Asset]] page to see all of your files in the [[Unlinked References]] section