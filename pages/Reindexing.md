alias:: reindex, refresh, refreshing

- _Reindexing_ does not manipulate your Markdown/Org Mode files but simply rebuilds Logseq's internal database based on your Markdown/Org Mode files.
- _Refreshing_ will update the content displayed in Logseq from the content stored in your Markdown/Org Mode files.
-
  #+BEGIN_WARNING
  **Loss of data**
  If, for some reason, the content displayed in Logseq is newer than the one on your disk, your content stored on your disk will be lost and replaced with the content from Logseq. A warning message is displayed when you attempt to reindex or refresh.
  **Always backup your data (from Logseq by exporting and from your disk by copying the file) before reindexing or refreshing.**
  #+END_WARNING
- **USAGE**
	- To _reindex_, click on your graph's name in the top right (next to the three dots) and select _Re-Index_
	- To _refresh_, click on your graph's name in the top right (next to the three dots) and select _Refresh_
- **EXAMPLES**
	- You have used an external text editor to make modifications to your files. You can use _Refresh_ to update Logseq with these changes.
	- You have updated your [[config.edn]] in an external text editor and want these changes to reflect in Logseq. You can use _Reindex_ to do so.