- Logseq stores a version history when editing your files.
- Version history is managed via [Git](https://git-scm.com/) as a version control system. Logseq uses an internal Git client so you do not need to have it installed on your system.
- Version history is optional. You can still use other ways to backup your data.
-
  #+BEGIN_CAUTION
  Do not use Logseq's Git version history (or Git in general) in conjunction with Dropbox, Google Drive or similar tools. Synchronization managed by these tools may conflict with Git's version management 
  #+END_CAUTION
-
  #+BEGIN_TIP
  You do not need to know anything about Git to use Logseq's version history capability.
  #+END_TIP
-
  #+BEGIN_WARNING
  If you already have a manually created Git repository in your [[graph]] directory, Logseq's Git integration will create commits for your _existing_ repository. You can still push to your remote location if you have specified one, or use it locally only.
  #+END_WARNING
- **USAGE**
	- Version history is enabled at _[[Settings]] > Version Control_
	- You can choose to save changes automatically or on-demand
		- Every 60 seconds (or as specified) a new version is created automatically (if there has been any change), or if _[[Settings]] > Version Control > Enable Git auto commit_ is disabled
		- Manually create a new version by hitting `c` (for <ins>c</ins>ommit) on your keyboard and entering a message to describe the change
	- You can run any custom Git commands, for example `git push` to _push_ your changes - i.e. update your remote repository -, via `Cmd+!` or `Alt+!`
		- Logseq does not automatically push your changes. You have to do it manually or use means that are independent of Logseq, for example [git post-commit hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
	- You can access your page history at the three dots menu of the page next to the page title at _Check page history_
		- To restore to a previous version, click on any entry, copy its content and replace your current page with it
	-
	-
	-