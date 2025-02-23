- Templates allow you to quickly use often used content types. You define a template block once, and can then use it in any other page or block.
-
  #+BEGIN_WARNING
  Templates simply copy text. They cannot contain any advanced logic.
  #+END_WARNING
- Templates support [[Dynamic Variables]].
- **USAGE**
	- To create a template
		-
		  1. Right click a block [[bullet]] and select `Make template`, or 
		  2. Add a page-level [[property]] `template:: myTemplate` (on the current page or another)
		- You can choose to include the parent block (via `template-including-parent:: true` [[property]]).
		-
		  #+BEGIN_TIP
		  It is easiest to use a single page to contain _all_ of your templates, and then have each template be a different block.
		  #+END_TIP
	- To use a template, use the `/Template` [[command]]
	- To update a template, simply change the content of the original template page.
	  #+BEGIN_TIP
	  Updates to a template page are not propagated to the instances where you have used the template.
	  #+END_TIP
	- To delete a template, simply remove the `template::` property.
	  #+BEGIN_TIP
	  Deleting a template page will not delete or modify any of the instances where you have used the template.
	  #+END_TIP
- **EXAMPLES**
	- This is the first line. It will be included in the template.
	  template:: my-test-template
		- This is a child line.
			- This is a grandchild line.
	- This is the first line. It will _not_ be included in the template.
	  template:: my-other-test-template
	  template-including-parent:: false
		- This is a child line.
			- This is a grandchild line.
## Default Templates in [[Journals]]
	- You can specify a default template for newly created [[Journal]] pages.
	- Change the `default-templates` section in [[config.edn]] to reference your template.
	- For example, you can create a template with `template:: my-default-template`, and change [[config.edn]] to:
	  ```clojure
	  :default-templates
	   {:journals "my-default-template"}
	  ```
	-
	  #+BEGIN_TIP
	  The name is the one you specify after `template::` and _not_ the page title.
	  #+END_TIP