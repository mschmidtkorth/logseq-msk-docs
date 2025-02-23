alias:: command

- Commands are used for Logseq-specific features.
- ## Basic Commands
	- Basic commands can be accessed by typing `/`.
	- [[References]]
	- Text formatting
		- `/Underline`
	- [[Files]]
	- [[Task Management]]
	- Admonitions (preformatted text blocks)
	  id:: 61111d75-fbc7-405e-a309-ac8a209ed9d9
		- `<Tip`
		- `<Important`
		- `<Caution`
		- `<Warning`
	- [[Queries/Advanced Queries]]
	- [[Zotero]]
	- [Query table functions](((610fdfba-d6cf-4bb1-a88d-b3fe28e0a72d)))
	- [[Slides]]
	- Calculator
		- Type `/Calculator` to enter any calculations.
		-
		  ```calc
		  42+3.141^2
		  ```
	- [[Drawings]]
	- Embedded videos or tweets from Twitter
		- You can embed tweets via `{{tweet https://twitter.com/barackobama/status/896523232098078720}}`
		- {{tweet https://twitter.com/barackobama/status/896523232098078720}}
	- [[Spaced Repetition]] cards and clozes
	- ## Advanced Commands
		- Advanced commands are added via `<`.
		- `<Src` for source code blocks; use `#+BEGIN_SRC javascript` to specify the language
		- Admonitions (preformatted text blocks)
		  id:: 61111d75-a7a0-4db7-aa57-1f697d5c5241
			- `<Tip`
			  #+BEGIN_TIP
			  A tip.
			  #+END_TIP
			- `<Important`
			  #+BEGIN_IMPORTANT
			  Important.
			  #+END_IMPORTANT
			- `<Caution`
			  #+BEGIN_CAUTION
			  Caution.
			  #+END_CAUTION
			- `<Warning`
			  #+BEGIN_WARNING
			  Warning.
			  #+END_WARNING
			- `<Example` preserves whitespace and prevents Markup formatting, typically used for source code
			  #+BEGIN_EXAMPLE
			  Example.
			  #+END_EXAMPLE
			- `<Verse` preserves newlines
			  #+BEGIN_VERSE
			  A verse.
			  Another verse.
			  #+END_VERSE
		- Drawers
			- Drawers are a way of managing information - typically _metadata_, i.e. not actual content - in a collapsible section, that is in context to its parent block.
			- They are originally a [feature](https://orgmode.org/manual/Drawers.html) from [[org-mode]].
			- Drawers
				- are created automatically for repeating tasks whenever you mark the task as done (`:LOGBOOK:`). This allows you to track your task history without disturbing your document.
					- TODO Do something regularly
					  SCHEDULED: <2021-08-31 Tue .+1d>
					  :LOGBOOK:
					  - STATE: "DONE" FROM "TODO" 2021-08-29T23:05:37
					  :END:
				- can be created manually via the following syntax:
				  ```
				  :nameOfYourDrawer:
				  My hidden content
				  :END:
				  ```
					-
					  :nameOfYourDrawer:
					  My hidden content
					  :END: