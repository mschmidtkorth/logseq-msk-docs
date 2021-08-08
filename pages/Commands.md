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
			- `<Example` preserves whitespace
			  #+BEGIN_EXAMPLE
			  Example.
			  #+END_EXAMPLE
			- `<Verse` preserves newlines
			  #+BEGIN_VERSE
			  A verse.
			  Another verse.
			  #+END_VERSE