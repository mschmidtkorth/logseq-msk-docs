- Zotero is tool to manage literature references typically used by people working in academia.
- It is free and easy-to-use and helps you to collect, organize, cite, and share research.
- Logseq has a built-in Zotero integration to import your Zotero library items as Logseq pages.
  #+BEGIN_WARNING
  **Requirements**
  The Zotero integration requires using the _Zotero Sync_. This free functionality stores your library items on Zotero server.
  If you are not using Zotero Sync enabled, you could use 
  1. [logseq x zetero](https://github.com/aljedaxi/logseq-zotero/), a third-party [[plugin]] for Logseq. The plugin is going to access your local Zotero library and store it in Markdown files. You can then simply reference these Markdown files as you would any other Logseq page.
  1. [Zotero-mdnotes](https://argentinaos.com/zotero-mdnotes/), a third-party app to export your Zotero metadata to Markdown files. You can then simply reference these Markdown files as you would any other Logseq page.
  #+END_WARNING
- **USAGE**
	- One-time setup
		-
		  1. Go to [zotero.org](https://www.zotero.org/) and create a Zotero account (or use your existing one) 
		  1. [Download](https://www.zotero.org/) and install Zotero
		  1. Open the app and enable Zotero Sync at _Preferences > Sync_
		  1. Create a new private API key and note down your userID from that same page
		  #+BEGIN_WARNING
		  Do not share this API key with anyone.
		  #+END_WARNING 
		  5. Make sure to grant at least "Allow library access". If you want to include notes, make sure to grant "Allow notes access". You can keep any of the other default settings. 
		  (optional) If you've got [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/installation) installed, Logseq will use citation key as your page name, otherwise, it'll just use default item title as your page name.
		  Make sure to check [here](https://alix-lahuec.gitbook.io/zotero-roam/getting-started/prereqs) and follow the setup checklist to enable autoPinDelay and pin your existing citekeys. 
		  6. In Logseq, go to _[[Settings]] > Zotero settings_ and add your API credentials.
		  #+BEGIN_TIP
		  You can add multiple Zotero profiles in logseq, for example to separate between work and personal use or to use different devices or users (with different settings paths).
		  #+END_TIP
	- Using Zotero integration with Logseq
		-
		  1. Use the `/Zotero` [[command]] to search Zotero library items (by title, author, text, anything) and then add one as a Logseq page, or
		  1. (optional) Import _all_ of your Zotero library items at _[[Settings] > Add all Zotero items: Add all_
		-
		  #+BEGIN_NOTE
		  If you add/reference the same item twice/again, Logseq will append the data to the same page instead of overwriting your existing metadata. To replace it, you first have to delete the corresponding Markdown page.
		  #+END_NOTE
		-
		  #+BEGIN_TIP
		  **Zotero metadata updates**
		  If metadata is updated in Zotero, it will _not_ reflect automatically in Logseq. Only if you reference the same source again via `/Zotero` - this will append a new block to the initial [[page]] for the library item. In that way, the bottom block always reflects the most recently cited version of your Zotero library item. Previously cited items will not be updated. You may remove or keep them in your page.
		  #+END_TIP
		-
		  #+BEGIN_TIP
		  You do **not** need to manually sync Logseq with Zotero, this happens when you search for another item.
		  #+END_TIP
		-
		  #+BEGIN_TIP
		  **Using Zofiles**
		  You can also reference [ZotFiles](http://zotfile.com/) stored on your machine. To do that, set the Logseq base directory to the path where you store your files at _[[Settings]] > Editor > Zotero Settings > Linked Attachment Base Directory_.
		  #+END_TIP
		-
		  #+BEGIN_TIP
		  **Using attached files**
		  You do **not** need to copy your files (e.g. a PDF document) to Logseq's `/asset/` directory - it is imported automatically when referencing a Logseq item.
		  If you want to reference external PDFs, you can use the `/asset` [[command]].
		  #+END_TIP.
		-
		  #+BEGIN_TIP
		  **Using relative links**
		  You can use relative links instead of absolute links by specifying the _Zotero Data Directory_ for imported attachments or _Linked Attachment Base Directory_ for linked attachments at _[[Settings]] > Editor > Zotero Settings (requires re-importing the Zotero item).
		  #+END_TIP
		- Logseq will add a prefix to all imported Zotero items to easily search for them. The default prefix is `@`, you can change it in _[[Settings]] > Zotero settings_. You can also put any Zotero reference as a child-page by creating a hierarchy via `Zotero/`.
		- As usual, because the items are going to be created as pages, you can reference them wherever you would like to indicate the library item as a source. Of course, you can also add your own content or additional properties to the page.
			- [[@IEEE Style Manual]]
		- You can see all references for a specific highlight by right-clicking it in the PDF and selecting _Linked references_