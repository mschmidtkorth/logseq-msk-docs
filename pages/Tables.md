alias:: table

- You can use tables to show structured information.
- **USAGE**
	- To add a table you need to write it as text. Each row is put on its own line (within the same [[block]]) and each column is separated by a vertical line (`|`).
- **EXAMPLE**
	-
	  |Column A|Column B|Column C|
	  |Text|More text|And even more|
	  |Text|More text|And even more|
	-
	  ```source
	  |Column A|Column B|Column C|
	  |Text|More text|And even more|
	  |Text|More text|And even more|
	  ```
-
  #+BEGIN_WARNING
  * Tables cannot be sorted.
  * Tables do not support line breaks or lists. As an alternative, you may use [Kanban view](https://discuss.logseq.com/t/css-trigger-columns-kanban-view-with-tags/390) or [hiccups](60f48a7d-b083-4d92-961e-8912025e6cd8) to insert HTML line breaks
  ```md
  |Column|Column[:br]Second line|
  ```
  |Column|Column[:br]Second line|
  #+END_WARNING