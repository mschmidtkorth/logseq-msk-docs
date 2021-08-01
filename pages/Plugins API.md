alias:: plugin, plugins

- [Documentation](https://logseq.github.io/plugins/index.html)
- A plugin is just a web page using some Logseq-provided APIs. You can use **any language** or programming framework, frameworks, and tools, as long as they can be used to build a webpage.
- To update the plugin API: `npm i @logseq/libs@latest`
-
  #+BEGIN_WARNING
  Slash commands work differently if a block is opened in the sidebar - then, some functions like `logseq.Editor.getCurrentPage()` return `null`.
  #+END_WARNING
## Initial Setup
	- Clone [plugin repository](https://github.com/logseq/logseq-plugin-samples)
	- Open _Logseq > Settings: Enable Developer Mode_
	- `cd` into cloned plugin folder, e.g. `logseq-hello-world`
	- `npm i && npm run build` (depending on plugin Readme) to generate the `dist/` folder
	  collapsed:: true
		- `npm run build` generates `/dist/index.html` which is referenced by `package.json`
	- Open _Logseq > Plugins Select folder_
	- Restart Logseq if needed
	- Description, title etc. of plugin is taken from `package.json`
## Updates to code
	- Update code and then run `npm run build` again to refresh `/dist`, then toggle the plugin in Logseq
	- For newly registered slash commands, you have to restart Logseq once
	- For any HTML elements to be shown, execute `logseq.showMainUI()` to show the plugin's UI; you can also investigate the HTML code via Developer Console (search for `index.html`'s content, e.g. `id="app"`)
## Packaging plugins
	-
	  1. Clear the `dist` folder (otherwise you will get multiple versions)
	  1. `npm run build` and copy the `dist` folder
	  1. Add `README.md`, `logo.png`, `package.json`
	  1. zip and distribute
## Considerations
	- Plugins cannot be used to manipulate or replace blocks. You can trigger them via slash commands or block commands.
	- Plugins are isolated containers - you cannot reference elements outside of the plugin's scope without using the API
		- Therefore, you also cannot use e.g. the tailwindCSS plugin from the Logseq app, you need to import it yourself
	- Logseq's API methods are asynchronous; in Javascript use `await` and wrap them in a `async` method
	  ```js
	  methods: {
	  	async scrollTo(id) {
	  		const { name } = await logseq.Editor.getCurrentPage();
	  
	  		logseq.Editor.scrollToBlockInPage(
	  			name, // name of page
	  			id // into block uuid
	  		);
	  	},
	  },
	  ```
	- Example
	  ```js
	  const pageId = await logseq.Editor.getCurrentPage() // IEditorProxy becomes Editor, IAppProxy becomes App etc. - use IntelliSense!
	  const test = await logseq.Editor.getPageBlocksTree(pageId)
	  ```
	- Creating notifications
	  ```js
	  console.log('toc', 'Hello, this is ToC for page:', await logseq.Editor.getCurrentPage());
	  // Show notification (just for testing purposes)
	  const { content, uuid } = await logseq.Editor.getCurrentBlock();
	  logseq.App.showMsg(`
	  		[:div.p-2
	  		[:h1 "Displaying ToC"]
	  		[:h2 "Block #${uuid}"]
	  		[:.text-sm "${content}"]]
	  	`);
	  ```
	  #+BEGIN_WARNING
	  Notifications add a full width layer on top - until they disappear, you cannot interact with the page/content below
	  #+END_WARNING