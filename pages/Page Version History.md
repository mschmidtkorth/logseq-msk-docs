- Logseq stores a version history when editing your files.
- Version history is managed via [Git](https://git-scm.com/) as a version control system. Logseq uses an internal Git client so you do not need to have it installed on your system.
-
  #+BEGIN_TIP
  You do not need to know anything about Git to use Logseq's version history capability.
  #+END_TIP
- **USAGE**
	- Version history is enabled at _[[Settings]] > Version Control_
	- You can choose to save changes automatically or on-demand
		- Every 60 seconds (or as specified) a new version is created automatically (if there has been any change), or if _[[Settings]] > Version Control > Enable Git auto commit_ is disabled
		- Manually create a new version by hitting `c` (for <ins>c</ins>ommit) on your keyboard and entering a message to describe the change
	- You can run any custom Git commands, for example `git push` to _push_ your changes - i.e. update your remote repository -, via `Cmd+!` or `Alt+!`
	- You can access your page history at the three dots menu of the page next to the page title at _Check page history_
		- To restore to a previous version, click on any entry, copy its content and replace your current page with it
	-
	-
	-