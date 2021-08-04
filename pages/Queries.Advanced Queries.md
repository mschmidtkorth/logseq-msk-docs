- [Documentation](https://logseq.github.io/page/Queries#/page/advanced%20queries)
- **USAGE**
	- Advanced queries are written via [Datalog](https://en.wikipedia.org/wiki/Datalog) with Clojure syntax
## Query Toggles
	- There are certain properties that allow you to control the output of advanced queries.
	- **USAGE**
	- `:collapsed?` determines whether the query results are collapsed (`true`) or expanded (`false`) by default
	- `:breadcrumb-show?` determines whether to show breadcrumbs in a query result (i.e. the path to the block)
	- **EXAMPLE**