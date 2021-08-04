testproperty:: My value
tags:: myPageTag

- [Documentation](https://logseq.github.io/page/Queries#/page/queries)
- **USAGE**
  section:: Usage
	- You can create simple queries via the `/Query` [[Command]]
	- The syntax for simple queries is `{{query (<details>)}}`
- **EXAMPLES**
	- ## General
		- Limit the results to those part of the current page
		  query-table:: false
		  {{query (and (page <% current page %> block-property section Usage))}}
		- Use multiple conditions (or) - only works for text
			- {{query myTag my-other-tag}}
			  query-table:: true
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