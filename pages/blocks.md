alias:: block

- Blocks are the smallest entities in Loqseq. Blocks are indicated by [[bullets]] on the left. Each [[page]] has at least one block.
- **USAGE**
	- Whenever you hit `Return` a new block is created. You can create a new line within the same block by hitting `Shift+Return`.
	- Blocks can have any number of (nested) sub-blocks. The root of a block is always a page (which is simply a block itself).
	- Blocks are used to group closely related units of information and the major differences to traditional word processing tools.
	- Blocks can be _embedded_ in another location (directly editable, will update everywhere) or _referenced_ (view only). Use the `/Block Embed` and `/Block Reference` [[commands]].
	- You can easily move blocks via drag & drop
		- You can use `opt+drag` to create a reference to a block.
		  id:: 61111d74-7e0a-4b1e-90f9-733ab71c1b7e
	-
	  #+BEGIN_WARNING
	  You cannot convert a block to a page.
	  #+END_WARNING
	- You can convert blocks to headings or add a highlight color by right-clicking the block [[bullet]].
	-
	  #+BEGIN_NOTE
	  Each block has an automatically generated unique identifier (UUID) with a length of 32 and four hyphens. Logseq uses them to identify a block, for example, when referencing it.
	  #+END_NOTE
- **EXAMPLES**
	- This is a block.
	  This is still the same block.
		- This is a sub-block.
		  id:: 6106b8e8-2a72-402f-8de1-ed319bbf0110
			- This is a block with block [[properties]].
			  type:: special-block
	- This is a reference: ((6106b8e8-2a72-402f-8de1-ed319bbf0110))
	- This is an embedded block:
	  {{embed ((6106b8e8-2a72-402f-8de1-ed319bbf0110)) }}
	- This is a heading block
	  heading:: true
	- This is a highlighted block
	  background-color:: #793e3e