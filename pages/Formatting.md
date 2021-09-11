- You can use formatting for your text similar to any other word processing application.
  id:: 612a2413-0d44-4539-be1f-ba538fc520fa
-
  #+BEGIN_TIP
  See also [simple](((61111d75-fbc7-405e-a309-ac8a209ed9d9))) and [advanced](((61111d75-a7a0-4db7-aa57-1f697d5c5241))) admonition blocks.
  #+END_TIP
- **USAGE & EXAMPLES**
	- Use [[commands]] or simply type the formatting syntax
	- Links
	  id:: 612a2437-103f-4c3f-bd99-2a98a462b6c2
		- [External link](https://github.com/mschmidtkorth/logseq-msk-docs) via `[External link](https://github.com/mschmidtkorth/logseq-msk-docs)`
		- [[Page reference]] via `[[Page reference]]`
		- ![Page reference with label](Task Management) via `![Page refernece with label](Task Management)`
		- [Page reference with label]([[Task Management]]) via `[Page refernece with label]([[Task Management]])`
		- ![PDF file link](../assets/IEEE-StyleManual_1628420481975_0.pdf) via `![PDF file link](../assets/IEEE-StyleManual_1628420481975_0.pdf)`
		- [Block reference with label](((612a2413-0d44-4539-be1f-ba538fc520fa))) via `[Block reference with label](((612a2413-0d44-4539-be1f-ba538fc520fa)))`
	- [Priorities]([[Task Management]])
		- [#A] Important via `[#A] Important`
		- [#B] Less important via `[#B] Less important`
		- [#C] Even less important via `[#C] Even less important`
	- [[HTML]]
	- Formatting
		- **Bold** via `**Bold** `
		- _Italic/cursive_ via `_Italic/cursive_`
		-
		  <ins>Underline</ins> via `<ins>Underline</ins>`
		- ~~Strikethrough~~ via `~~Strikethrough~~`
		- ^^Highlight^^ via `^^Highlight^^`
	- Lists
		- Ordered list
			-
			  1. Item 1
			  2. Item 2
			  3. Item 3
				-
				  ```md
				  1. Item
				  2. Item
				  3. Item
				  ```
			- Or simply
				-
				  ```md
				  1. Item
				  1. Item
				  1. Item
				  ```
		- Unordered list (in multiple blocks, the usual way to create lists)
			- Item 1
			- Item 2
			- Item 3
		- Unordered list (in single block)
			-
			  * Item 1
			  * Item 2
			  * Item 3
				- ```md
				  * Item 1
				  * Item 2
				  * Item 3
				  ```
			-
			  #+BEGIN_TIP
			  Unordered lists in single blocks can also be used for lists in admonition blocks (e.g. quote or tip blocks - both [simple](((61111d75-fbc7-405e-a309-ac8a209ed9d9))) and [advanced](((61111d75-a7a0-4db7-aa57-1f697d5c5241)))).
			  #+END_TIP
	- `code` via \`code\`
		-
		  ```plain
		  More code
		  ```
			- via 
			  ```
			  \```plain
			  More code
			  \```
			  ```
	- Headings
		- Via `#` (add additional `#` to increase heading number from large to small)
		- # Level 1
			- ## Level 1.1
		- # Level 2
		  heading:: true
			- ## Level 2.1
				- ### Level 2.1.1
	- [[Tables]]
	- Ruler via `---`
	-
	  ---
	- $\LaTeX$ via `$a^2+b^2=c^2$`
		- $a^2+b^2=c^2$
