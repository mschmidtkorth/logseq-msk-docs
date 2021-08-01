alias:: alias

- Sometimes the same thing has different names. You can use _aliases_, a type of [[properties]], for pages to create links from multiple origins to the same page.
- **USAGE**
	- Aliases must be defined in a [[properties]] [[block]] at the top of a [[page]].
	- The syntax is similar to [frontmatter](https://www.gatsbyjs.com/docs/how-to/routing/adding-markdown-pages/#:~:text=%2D1.md%20.-,Frontmatter%20for%20metadata%20in%20Markdown%20files,and%20end%20of%20the%20block.) used in Markdown files.
- **EXAMPLE**
	- Let's assume you have a page with information about smartphones - called [[smartphone]]. You also want to bring up the same page when linking [[phone]] or [[mobile phone]].
		- At the top of your `smartphone` page - your _original_  - you add a block with properties:
		  alias:: phone, mobile phone
	- Let's assume you have a page about the [[European Union]] - but sometimes you use the acronym [[EU]].
		- At the top of your `European Union` page - your _original_  - you add a block with properties:
		  alias:: EU
-
  #+BEGIN_WARNING
  * Logically you cannot use aliases for blocks.
  * Aliases show separately (isolated, like satellites) on the [[graph]] and will not have any links.
  #+END_WARNING
-
  #+BEGIN_TIP
  When using multiple aliases, add a _space_ after the comma.
  #+END_TIP
-
- Aliases and conflicting page names
	- Let's assume you created a page `smartphone` with an alias `phone`. However, before you created this page you already had created the (blank) `phone` page - which is now redundant.
	- You now want to clear up the duplicate and only keep `smartphone`. What happens if you _delete_ the second page `phone`?
	- In the source Markdown files, nothing is going to change. Only the _database_ Logseq uses internally gets updated, but any references are kept (they may require a [[Reindexing]]).