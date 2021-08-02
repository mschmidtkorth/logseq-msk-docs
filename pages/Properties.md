alias:: Property

- Properties are key-value pairs that allow you to annotate a block or page
	- _Page properties_ are defined by putting them into the first block of the page (_[[frontmatter]]_)
	- _Block properties_ are defined by putting them into any other block
	- When a property value matches an existing page title, Logseq will automatically create a link to that page
		- TODO This is not working for me
	- When a property contains commas (`,`), any values are going to be automatically linked, even if the pages may not exist:
	  ```
	  parts:: motor, steering wheel, tyres
	  ```
		-
		  parts:: motor, steering wheel, tyres
	- When a property contains references, (`[]`), any values are going to be automatically linked:
	  ```
	  parts:: [[motor]] and other parts
	  ```
		-
		  parts:: [[motor]] and other parts
	-
	  #+BEGIN_TIP
	  To prevent values from being auto-linked, wrap _all_ values within quotes (`"`) - for example, `parts:: "[[motor]], steering wheel, tyres"`
	  You cannot quote (unlink) _parts_ (items) of a list property, e.g. `parts:: [[motor]], "steering wheel, tyres"` is not going to prevent values from being linked - see [feature request](https://discuss.logseq.com/t/property-values-with-a-mix-of-references-and-unlinked-text/1720))
	  #+END_TIP
	- Pages mentioned as property values get backlinked.
- **USAGE**
	- A page can have _many_ pairs of properties (the collection is a user-defined dictionary) as long as they are in first block of that page
	  ```
	  type:: documentation
	  parts:: motor, steering wheel, tyres
	  ```
	- Each block may also have _many_ pairs of properties (except for the first block, which will be served as page properties)
	- Properties (key-value pairs) can be added via [[frontmatter]]-like syntax for a page (first block of the page) or a block:
	  ```
	  type:: [[book]]
	  author:: [[sönke ahrens]]
	  publication_date:: [[february 21, 2017]]
	  ```
	- Properties have two **use cases**
		- Selecting ([[querying]]) specific pages/blocks:
			- For example, let's query all the blocks with the property `parts` and the value `steering wheel`:
			  query-sort-by:: block
			  query-table:: false
			  query-sort-desc:: true
			  {{query (property parts "steering wheel")}}
			- Or simply get all the blocks with the property `parts
			  {{query (property parts)}}
			- We can also use [[Queries/Advanced Queries]]:
				-
				  #+BEGIN_SRC clojure
				   #+BEGIN_QUERY
				   {:title [:h2 "My books"]
				    :query [:find (pull ?b [*])
				   :where
				   [?b :block/properties ?p]
				   [(get ?p :type) ?t]
				   [(= "[[book]]" ?t)]]}
				   #+END_QUERY
				   #+END_SRC
				-
				  #+BEGIN_QUERY
				  {:title [:h2 "My steering wheel blocks"]
				   :query [:find (pull ?b [*])
				  :where
				  [?b :block/properties ?p]
				  [(get ?p :parts) ?t]
				  [(= "[[steering wheel]]" ?t)]]}
				  #+END_QUERY
		- Providing common attributes to your pages/block - for example, you could have a template `Book` and a list of attributes you want to define for each book:
		  ```
		  author: [[george polya]]
		  title: Mathematics and Plausible Reasoning
		  published: 2009
		  ```
- ## Special Properties
	- There are special properties that control Logseq functionality (the number in brackets indicates how many values you may define):
		- `tags` (N) get listed in their own section "Pages tagged with X" below a page.
		- `template` (1) designates a page as a template.
		- `template-including-parent` (1) (in previous versions `include-parent`) specifies whether the parent level content of the selected block should be included when using a template
		- `collapsed` (1) specifies whether a block is collapsed.
		- `alias` (N) define synonyms for a page.
		- `id` (1) specifies an [Id](https://discuss.logseq.com/t/what-are-id-links-vs-block-ids-vs-page-ids/1318/2) for org mode.
		- `title` (1) overrides the title of a page to be different from the file name.
		- `created-at` (1) and `updated-at` (in previous versions `last-modified-at`) (1) define the date/time stamps in [Unix time](https://en.wikipedia.org/wiki/Unix_time); block-level only.
		- `parent` (1) references the parent block (could be a page).
		- `query-table` (1) will mark a query to be shown as the table view.
		- `query-properties` (N) stores a user's custom properties to be shown for a query table.
		- `filters` (N, object with booleans) store selected filters for linked references on page-level.
		- `public` (boolean) defines whether a page should be included in an export.