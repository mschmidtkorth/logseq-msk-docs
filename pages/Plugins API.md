alias:: plugin, plugins

- [Documentation](https://logseq.github.io/plugins/index.html)
- Logseq's functionality can be enhanced via community-provided plugins.
- Technically, a plugin is just a web page using some Logseq-provided functions via its interface (API). You can use _any language_, programming framework, or tool, as long as they can be used to build a webpage.
## Using Third-Party Plugins
	-
	  #+BEGIN_CAUTION
	  Be careful with third-party plugins and only use those from trusted sources. 
	  #+END_CAUTION
	- ### Installing Plugins
		- This section is about installing provided plugins to Logseq. If you want to develop your own plugin, see [below](((610afd9b-1224-453c-b753-b16cc3a88ad8))).
		- Plugins are typically distributed via GitHub repositories. There are two options of installing such a plugin:
		  1. Downloading a pre-compiled version from the _Releases_ section
		  1. Compiling it yourself from the source code (requires some technical expertise)
		- To install from source code
			- Check the Readme for the plugin - it typically follows instructions listed [below](((610afd9b-1224-453c-b753-b16cc3a88ad8)))
		- To install a downloaded plugin
			- Open _Logseq > [[Settings]]: Enable Developer Mode_ to generally enable plugin functionality
			  id:: 61111d75-0a16-4911-8934-dafed3a0fa67
			- Restart Logseq
			  id:: 61111d75-0ead-4fb6-ae2b-172cffee16ae
			- Open _Logseq > three dots menu > Plugins > Load unpackaged plugin > Select folder_
			  id:: 61111d75-063e-4410-935f-d9f5e5c55f71
			- Restart Logseq if needed
- ## Developing Your Own Plugins
	- ### Initial Setup for Development
	  id:: 610afd9b-1224-453c-b753-b16cc3a88ad8
		- Clone [plugin repository](https://github.com/logseq/logseq-plugin-samples)
		- Open _Logseq > [[Settings]]: Enable Developer Mode_ to generally enable plugin functionality
		- Restart Logseq
		- `cd` into cloned plugin folder, e.g. `logseq-hello-world`
		- `npm i && npm run build` (depending on plugin Readme) to generate the `dist/` folder
		  collapsed:: true
			- `npm run build` generates `/dist/index.html` which is referenced by `package.json`
		- Open _Logseq > Plugins > Load unpackaged plugin > Select folder_
		- Restart Logseq if needed
		-
		  #+BEGIN_TIP
		  Description, title etc. of a plugin are taken from `package.json`.
		  #+END_TIP
	- ### Updating the Plugin API library
		- Use `npm i @logseq/libs@latest`
	- ### Updates to Code
		- Update your code and then run `npm run build` again to refresh `/dist`, then toggle the plugin in Logseq
		- For newly registered slash commands, you have to restart Logseq once
		- For any HTML elements to be shown, execute `logseq.showMainUI()` to show the plugin's UI; you can also investigate the HTML code via Developer Console (search for `index.html`'s content, e.g. `id="app"`)
	- ### Packaging Plugins
		- To distribute  a plugin
			-
			  1. Clear the `dist` folder (otherwise you will get multiple versions)
			  1. `npm run build` and copy the `dist` folder
			  1. Add `README.md`, `logo.png`, `package.json`
			  1. zip and distribute
	- ### Considerations
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
		-
		  #+BEGIN_WARNING
		  Slash commands work differently if a block is opened in the sidebar - then, some functions like `logseq.Editor.getCurrentPage()` return `null`.
		  #+END_WARNING
- ## Custom Themes
  id:: 61225f50-3c64-4b85-beed-fb87f65655ee
	- Themes can either be used by updating your `custom.css` file or as a plugin.
	-
	  #+BEGIN_TIP
	  Use either your `custom.css` file or a loaded plugin, otherwise you may have conflicting styling.
	  #+END_TIP
	- **USAGE**
		- ((61111d75-0a16-4911-8934-dafed3a0fa67))
		- ((61111d75-0ead-4fb6-ae2b-172cffee16ae))
		- ((61111d75-063e-4410-935f-d9f5e5c55f71))
		- Choose the theme at _three dots menu > Themes_
		- To develop a theme plugin, all you need to do is create a `package.json`
			-
			  ```json
			  {
			      "name": "MSK Enhanced",
			      "author": "Michael Schmidt-Korth",
			      "version": "0.0.1",
			      "description": "An enhanced version of the default theme.",
			      "logseq": {
			        "themes": [
			          {
			            "name": "MSK Enhanced",
			            "url": "./msk-enhanced.css",
			            "description": "An enhanced version of the default theme."
			          }
			        ],
			        "id": "msk_theme-enhanced",
			        "icon": "./msk-enhanced.png"
			      }
			    }
			  ```