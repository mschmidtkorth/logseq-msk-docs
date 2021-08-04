- Sometimes Markdown is not enough to represent your content. You can use HTML to help you or embed external websites.
- To insert custom HTML
  1. Directly write HTML code, or
  1. Use [hiccup](https://github.com/weavejester/hiccup/wiki/Syntax). This is a library, unrelated to Logseq, that allows you to describe HTML in a different syntax (it adds _syntax sugar_) and more concise way.
- **USAGE**
	- To write HTML code, type `/` and select `Embed HTML` or directly type `@@html: @@` - alternatively, you can type HTML code directly
	- To use hiccup, directly type it
- **EXAMPLE**
	- HTML
		- @@html: This text is written <sub>subscript</sub>@@
		- This is a meter <meter max="10" value="4" />
		- _Note:_ Do not put a space between `@@`, it is just used to avoid the HTML being parsed and not rendered visible below.
		  ```source
		  @ @html: This text is written <sub>subscript</sub>@@
		  This is a meter <meter max="10" value="4" />
		  ```
	- hiccup
		- (1) Custom with a plain `span` elements (change the `:width` attribute value to modify the progress)
		  [:span {:style {:background "#eeeeee" :width "100px" :height "0.5em" :display "inline-block" :border-radius "4px" :position "relative"}} [:span {:style {:background "#2b8a3e" :width "26%" :height "0.5em" :display "inline-block" :border-radius "4px" :position "absolute"}}]]
		  (2) With a `progress` element
		  [:progress {:max "15" :value "4"}]
		  (3) With an `input[type="range"]` element
		  [:input {:type "range" :value "3" :max "15"}]
		-
		  ```clojure
		  (1) Custom
		  [:span {:style {:background "#eeeeee" :width "100px" :height "0.5em" :display "inline-block" :border-radius "4px" :position "relative"}} [:span {:style {:background "#2b8a3e" :width "26%" :height "0.5em" :display "inline-block" :border-radius "4px" :position "absolute"}}]]
		  (2) With progress
		  [:progress {:max "15" :value "4"}]
		  (3) With input[type="range"]
		  [:input {:type "range" :value "3" :max "15"}]
		  ```
		- You can even embed external websites as iFrames
		  ```clojure
		  [:iframe {:src "https://logseq.github.io" :style {:height 800 :width 615}}]
		  ```