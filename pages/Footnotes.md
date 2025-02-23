alias:: footnote

- You can add additional information to your text with footnotes.
- **USAGE**
	- To use footnotes, you simply add the footnote indicator (marker) at the end of your text. Then, somewhere further down on the page, you add the footnote text for the marker.
	- The syntax for footnotes is similar to how they work in traditional Markdown.
	-
	  #+BEGIN_TIP
	  The footnote text may appear appear
	  * on the same block as the footnote (could be on a new line)
	  * in a block below on the same level (_sibling_)
	  * in a block below indented further (_child_)
	  * in an unrelated block
	  #+END_TIP
- **EXAMPLES**
	- The footnote itself is placed first.[^1] You can click on the number to jump to the footnote text.
	- Then, the footnote text is placed where you want the long text to appear:
	-
	  [^1]: This is the footnote text. You can click on the arrow to jump back to the origin.
	-
	  ```source
	  The footnote itself is placed first.[^1] You can click on the number to jump to the footnote text.
	  [^1]: This is the footnote text. You can click on the arrow to jump back to the origin.
	  ```