- While Logseq is using Markdown files, it provides additional features.
- **USAGE**
	- Type `<` and then select one of the predefined blocks.
- **EXAMPLES**
	-
	  #+BEGIN_TIP
	  The blocks starting with `#+BEGIN_` and ending with `#+END_` are syntax taken over from [org mode](https://orgmode.org/manual/Paragraphs.html) to also work in Markdown mode.
	  #+END_TIP
	- Note: The space between `# +#` and backticks has only been added to prevent rendering.
	-
	  #+BEGIN_QUOTE
	  A quote.
	  With multiple lines.
	  #+END_QUOTE
	-
	  ```source
	  # +BEGIN_QUOTE
	  A quote.
	  # +END_QUOTE
	  ```
	-
	  ``` source
	  Code.
	  ```
	-
	  ``` source
	  ` ``
	  Code.
	  ` ``
	  ```
		-
		  #+BEGIN_TIP
		  To quickly edit code, put the cursor within the code box and press `Esc`.
		  #+END_TIP
	- [[Queries/Advanced Queries]]
	- $\LaTeX$
	-
	  #+BEGIN_EXPORT latex
	  a^2+b^2=c^2
	  #+END_EXPORT
		-
		  #+BEGIN_TIP
		  You can also write LaTeX via
		  `$a^2+b^2=c^2$`
		  $a^2+b^2=c^2$
		  or `$$a^2+b^2=c^2$$` (will center)
		  $$a^2+b^2=c^2$$
		  #+END_TIP
	-
	  ```source
	  # +BEGIN_EXPORT latex
	  a^2+b^2=c^2
	  # +END_EXPORT
	  ```
	-
	  #+BEGIN_NOTE
	  A note.
	  #+END_NOTE
	-
	  ``` source
	  # +BEGIN_NOTE
	  A note.
	  # +END_NOTE
	  ```
	-
	  #+BEGIN_TIP
	  A tip.
	  #+END_TIP
	-
	  ```source
	  # +BEGIN_TIP
	  A tip.
	  # +END_TIP
	  ```
	-
	  #+BEGIN_IMPORTANT
	  An important note.
	  #+END_IMPORTANT
	-
	  ``` source
	  # +BEGIN_IMPORTANT
	  An important note.
	  # +END_IMPORTANT 
	  ```
	-
	  #+BEGIN_CAUTION
	  A message of caution.
	  #+END_CAUTION
	-
	  ``` source
	  # +BEGIN_CAUTION
	  A message of caution.
	  # +END_CAUTION 
	  ```
	-
	  #+BEGIN_PINNED
	  A pinned message.
	  #+END_PINNED
	-
	  ```source
	  # +BEGIN_PINNED
	  A pinned message.
	  # +END_PINNED
	  ```
	-
	  #+BEGIN_WARNING
	  A warning.
	  #+END_WARNING
	-
	  ``` source
	  # +BEGIN_WARNING
	  A warning.
	  # +END_WARNING 
	  ```
	-
	  #+BEGIN_EXAMPLE
	  An example.
	  #+END_EXAMPLE
	-
	  ```source
	  # +BEGIN_EXAMPLE
	  An example.
	  #+END_EXAMPLE
	  ```
	-
	  #+BEGIN_EXPORT ascii
	   _        _______  _______  _______  _______  _______ 
	  ( \      (  ___  )(  ____ \(  ____ \(  ____ \(  ___  )
	  | (      | (   ) || (    \/| (    \/| (    \/| (   ) |
	  | |      | |   | || |      | (_____ | (__    | |   | |
	  | |      | |   | || | ____ (_____  )|  __)   | |   | |
	  | |      | |   | || | \_  )      ) || (      | | /\| |
	  | (____/\| (___) || (___) |/\____) || (____/\| (_\ \ |
	  (_______/(_______)(_______)\_______)(_______/(____\/_)
	  #+END_EXPORT
	-
	  #+BEGIN_EXPORT
	  asd
	  #+END_EXPORT
	-
	  #+BEGIN_EXPORT
	  Centered text.
	  #+END_EXPORT