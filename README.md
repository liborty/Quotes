# Quotes
**(C) Libor Spacek, 2019**

Unix/Linux shell script utility to typeset quotation marks in proper English or Czech language styles and to convert plain text or markdown to most formats required by publishers.

### Motivation
Proper typesetting is fiddly business. Mostly one wants to avoid spending a lot of time and minute care on it, as with Latex  for example, or fiddling with hundreds of obscure buttons on common word-processors. The situation is even worse in some languages like Czech, where 'upstairs-downstairs' quotation marks are required but are not even present on keyboard layouts!

The recommended solution is to use *markdown* for easy  human input by the author(s). The fact that *markdown* is just plain text lends it equally well to easy machine processing by standard *Unix/Linux* utilities such as *sed* and *pandoc*. Thus the straight 'computer quotes' can be speed typed into the markdown file and quotes subsequently converts the text  into doc, odt or similar formats demanded by the publishers, with the quotation marks properly typeset. 

The difficult part was using sed to automatically determine which quote is to be the opening one and which the closing. It is not foolproof, i.e. if you mess up the input with isolated or multiple quote marks, expect the gigo (garbage in, garbage out) principle to kick in. Actually, space before an opening quote is more important than matching the pairs.

### Installation
- Requires  Unix/Linux type system with sed and pandoc installed. 
- Download the relevant shell script for your favourite language, make sure it is accessible (in your path) by placing it into a relevant bin directory and make it executable (*chmod u+x quotes-en*). Alternatively, run it from your current directory as *./quotes-en ...*.

### Usage Notes
	quotes-en filename format
	quotes-cz filename format
- reads any plain text (or markdown) from the input file, eg. */some/path/mynovel.md*
- writes the stylised and converted text in the target *format* to the current directory, eg. as mynovel.doc
- target output *format* will be typically odt or doc required by your publisher. The *format* is passed to *pandoc* so you can try any other pandoc output formats.
- Changes all "straight" 'computer' quotes to properly stylised English or Czech ones.
- Assumes that all opening quotes are preceded by a white space or a newline. 
- Note: single newlines are ignored by markdown, so they will disappear from the pandoc output. It took me a while to realise that this is a feature, not a bug.
- Single quotes are changed to double arrow (french) quotes in the Czech version.

**Example invocation:** quotes-en mynovel.md doc

**Todo:** 

- downgrading nested double quotes to singles. For now, explicitly deploy single quotes inside double ones, which is the correct author style anyway.
- cz version: upstairs-downstairs single quotes (as well as the french ones). Not sure if it is really needed.

**Gotcha:** Do not mix English and Czech text, or your English apostrophies will be turned into opening single quotes, which happen to be Czech closing single quotes. Confused? Too right you are. Just use the right shell for each language separately and then concatenate their outputs.