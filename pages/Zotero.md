- Zotero is tool to manage literature references typically used by people working in academia.
- It is free and easy-to-use and helps you to collect, organize, cite, and share research.
- Logseq has a built-in Zotero integration to import your Zotero library items as Logseq pages.
  #+BEGIN_WARNING
  **Requirements**
  The Zotero integration requires using the _Zotero Sync_. This free functionality stores your library items on Zotero server.
  If you are not using Zotero Sync enabled, you could use 
  1. [logseq x zetero](https://github.com/aljedaxi/logseq-zotero/), a 3rd-party plugin for Logseq. The plugin is going to access your local Zotero library and store it in Markdown files. You can then simply reference these Markdown files as you would any other Logseq page.
  1. [Zotero-mdnotes](https://argentinaos.com/zotero-mdnotes/), a 3rd-party app to export your Zotero metadata to Markdown files. You can then simply reference these Markdown files as you would any other Logseq page.
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
		  1. Make sure to grant at least "Allow library access". If you want to include notes, make sure to grant "Allow notes access". You can keep any of the other default settings.
		  Optional: 
		  If you've got [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/installation) installed, Logseq will use citation key as your page name, otherwise, it'll just use default item title as your page name.
		  Make sure to check [here](https://alix-lahuec.gitbook.io/zotero-roam/getting-started/prereqs) and follow the setup checklist to enable autoPinDelay and pin your existing citekeys. 
		  1. In Logseq, go to _[[Settings]] > Zotero settings_ and add your API credentials.
	- Using Zotero integration with Logseq
		-
		  1. Use the `/Zotero` [[command]] to search Zotero library items (by title, author, text, anything) and then add one as a Logseq page, or
		  1. Import _all_ of your Zotero library items at _[[Settings] > Add all Zotero items: Add all_
		-
		  #+BEGIN_NOTE
		  If you add the same item twice, Logseq will append the data to the same page instead of overwriting your existing metadata. To replace it, you first have to delete the corresponding Markdown page.
		  #+END_NOTE
		-
		  #+BEGIN_TIP
		  You do not need to manually sync Logseq with Zotero, this happens automatically after a few seconds.
		  #+END_TIP
		- Logseq will add a prefix to all imported Zotero items to easily search for them. The default prefix is `@`, you can change it in _[[Settings]] > Zotero settings_. You can also put any Zotero reference as a child-page by creating a hierarchy via `Zotero/`.
		- As usual, because the items are going to be created as pages, you can reference them wherever you would like to indicate the library item as a source. Of course, you can also add your own content or additional properties to the page.
		- [[@IEEE Style Manual]]
		- TODO Test what happens if metadata updated in Zotero