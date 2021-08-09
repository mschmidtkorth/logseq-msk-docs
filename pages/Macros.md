alias:: macro

- Macros (sometimes called _snippets_) are used to quickly insert text when you type a certain keyword.
- **USAGE**
	- Macros have no UI to be defined, they are created by adding them to the [[config.edn]] file in your [[Graph]] folder - there is a dedicated section `:macros {}`.
	- Each macro is placed on its own line.
	- Macros may contain Markdown or HTML syntax.
	- If you update a macro, focus the line where you are using the macro to refresh it.
	- To use a macro, type `{{{macroName}}}`. To pass parameters, type `{{{macroName param1, param2}}}`
- **EXAMPLES**
	- Define a macro to insert a link
	  ```clojure
	  :macros {
	  	"docLink" "[Documentation](https://github.com/mschmidtkorth/logseq-msk-docs)"
	  }
	  ```
	- Define a macro to insert today's date (via a [[Dynamic Variable]])
	  ```clojure
	  :macros {
	  	"today" "Today is **<% today %>**"
	  }
	  ```
	- Define a macro to insert HTML tags
	  ```clojure
	  :macros {
	  	"progress" "<progress value=\"50\" max=\"100\" />"
	  }
	  ```
	- Define a macro that inserts text at a specific location
	  ```clojure
	  :macros {
	  	"compare" "This is better than $1 and $2."
	  }
	  ```
	- Define multiple macros
	  ```clojure
	  :macros {
	  	"docLink" "[Documentation](https://github.com/mschmidtkorth/logseq-msk-docs)"
	  	"today" "Today is **<% today %>**"
	  	"progress" "<progress value=\"50\" max=\"100\" />"
	  	"compare" "This is better than $1 and $2."
	  	"gissue" "[Issue $1](https://github.com/mschmidtkorth/logseq-msk-docs/issues/$1)"
	  }
	  ```
	- {{{today}}}
	  {{{docLink}}}
	  {{{progress}}}
	  {{{compare Logseq, Roam Research, Obsidian}}}
	  {{{gissue 1}}}
	-
	  ```source
	  {{{today}}}
	  {{{docLink}}}
	  {{{progress}}}
	  {{{compare Logseq, Roam Research, Obsidian}}}
	  ```