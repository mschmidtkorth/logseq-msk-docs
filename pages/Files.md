alias:: images

- Information is not just text you add yourself. You may want to reference other documents.
- **USAGE**
	- Files can be attached to [[pages]] or [[blocks]] via the `/upload` command.
	- Any file you attach gets uploaded to the `/assets/` folder of your Logseq [[graph]] directory.
	- PDFs and other documents are previewed. You can disable it by adding a [[Custom CSS]] rule: `.pdf-preview { display: none }`
		- You can toggle the preview for individual files as well - `![label](url)` will display a preview (desktop app) while `[label](url)` only displays a clickable label
	- Images can be added simply by pasting them into a block.
	  #+BEGIN_TIP
	  If paste is not working, click outside the block, then focus it again and paste once more.
	  #+END_TIP