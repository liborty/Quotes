# Quotes
**(C) Libor Spacek, 2019**

Unix/Linux shell script utility to typeset quotation marks in proper Czech language style and to convert plain text or markdown to most formats required by publishers.

### Motivation

Proper typesetting is fiddly business. Mostly one wants to avoid spending a lot of time and minute care on it, as with Latex  for example, or fiddling with hundreds of obscure buttons on common word-processors. The situation is even worse in some languages like Czech, where 'upstairs-downstairs' quotation marks are required but are not even present on keyboard layouts!

The solution adopted here by Quotes is to use *markdown* for efficient human input. Additionally, the fact that it is just plain text lends it to easy machine processing by standard *Unix/Linux* utilities such as *sed* and *pandoc*. Thus the straight 'computer quotes' can be speed typed into the markdown file and Quotes subesquently converts the text  into .doc .odt or similar formats demanded by publishers, with the quotation marks properly typeset. 

The difficult part was using sed to automatically determine which quote is to be the opening one and which the closing. It is not foolproof, i.e. if you mess up the input with unmatched quotes, expect the gigo (garbage in, garbage out) principle to kick in.

### Installation
- Requires  Unix/Linux type system with sed and pandoc installed. 
- Then just copy the shell script, make sure it is accessible (in your path) by placing it into a relevant bin directory and make it executable (*chmod u+x quotes*). Alternatively, run it from your current directory as *./quotes ...*.

### Usage Notes
	quotes filename format
- reads any plain text (or markdown) from input file. The filespec should end with any standard format extension understood by *pandoc*, eg. */some/path/mynovel.mk*
- writes the stylised and converted text in the target *format* to the current directory, eg. as mynovel.doc
- target output *format* will be typically odt or doc required by publishers. The *format* is passed to *pandoc* so you can try any other pandoc output formats.
- Changes all "straight" 'computer' quotes to properly stylised Czech ones.
- Assumes that all (lower) opening quotes are preceded by a white space or a newline. Note: single newlines are ignored by markdown, so they will disappear from the pandoc output. It took me a while to realise that this is a feature, not a bug.
- Single quotes are changed to double arrow (french) quotes.

**Example invocation:** quotes mynovel.mk doc

**Todo:** downgrading nested double quotes to singles.
For now, explicitly deploy single quotes inside double ones, which is the correct author style anyway.

**Gotcha:** Do not mix English and Czech text, or your English apostrophies will get turned into Czech quotes! 

**Further work:** English version of Quotes.
