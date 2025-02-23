-
  #+BEGIN_PINNED
  This section is about exporting a static HTML/CSS/JavaScript version of your content to be hosted on a web server. You can also export 
  * all of your pages (your [[graph]]) as Markdown, OPML, or JSON by going to to _three dots menu > Export_
  * a single page as Markdown or OPML by going to _three dots page menu > Export _
  * a single block as Text, OPML, or HTML by right-clicking a block and selecting _Copy as_
  #+END_PINNED
- You can provide your Logseq knowledge base as a statically hosted website which can be hosted on GitHub pages or any other hosting provider.
-
  #+BEGIN_TIP
  Static exports require the desktop app.
  #+END_TIP
- A static export is precompiled and does not require a full web server as it is only HTML, CSS, Javascript and assets.
- **USAGE**
	- Open your [[graph]] in Logseq.
	- Decide whether you want to export _all_ of your pages or only _some_.
		- You want to export _all_ pages: Enable *[[Settings]] > Export all pages public when publishing.*
		- You want to export _specific pages_ only: Add a page [[property]] `public:: true` to each page you want to export. Do _not_ enable the setting above.
	- Go to _three dots menu > Export > Export Public Pages_.
	- Upload the result to your hosting provider or open them in your local server e.g. via `python -m SimpleHTTPServer` or `npm run serve`. As it is a static export you may open the resulting `index.html` file already locally to verify it.
	-
	  #+BEGIN_TIP
	  Static exports are read-only.
	  #+END_TIP
	-
	  #+BEGIN_WARNING
	  A export includes all of your content _as is_ - this means, that any properties such as whether blocks are collapsed or expanded are exported as well.
	  #+END_WARNING
- **TROUBLESHOOTING**
	- When clicking _Export_ files are generated but no success message is displayed. When opening `index.html` a blank page is opened or it loads forever.
		- If no success message is shown something went wrong.
		- Check your browser's developer tools for any JavaScript errors (console).
		- Make sure that any _assets_ you have referenced - images, PDFs etc. - actually exist in your `/assets/` folder. If not, remove the reference or add the missing binary file.
		- In order to identify the root cause, you may use _binary troubleshooting_ - move half of your `.md` files to a safe place and try exporting again. Repeat until the export is successful, then start adding back files one by one.
	-