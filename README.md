# Quotes
**(C) Libor Spacek, 2019**

Unix/Linux shell script utility to typeset quotation marks,  dashes and ellipsis in proper English or Czech language styles and to convert plain text or markdown to most formats required by publishers.

### Motivation
Proper typesetting is fiddly business. Mostly one wants to avoid spending a lot of time and minute care on it, as with Latex  for example, or fiddling with hundreds of obscure buttons word-processors. The basic problem is that certain common typographical elements like quotation marks and dashes are just not present on keyboard layouts in their proper forms.

The recommended solution is to use *markdown* for easy  human input by the author(s). The fact that *markdown* is just plain text lends it equally well to easy machine processing by standard *Unix/Linux* utilities such as *sed* and *pandoc*. Thus the straight 'computer quotes' and minus signs for dashes can be easily speed typed into the markdown file. This script then replaces them with the relevant  unicode characters and finally converts the document to doc, odt or similar formats demanded by the publishers. 

The difficult part was using sed to automatically determine which quote is to be the opening one and which the closing. It is not foolproof, i.e. if you mess up the input with isolated or multiple quote marks, expect the gigo (garbage in, garbage out) principle to kick in. Actually, white space before an opening quote is all that this script looks for, thus it is very fast. All other quotes are treated as closing quotes.

### Installation
- Requires  Unix/Linux type system with sed and pandoc installed. 
- Download the relevant shell script for your favourite language, make sure it is accessible (in your path) by placing it into a relevant bin directory and make it executable (*chmod u+x quotes-en*). Alternatively, run it from your current directory as *./quotes-en ...*.

### Usage Notes
	quotes-en filename format
	quotes-cz filename format
- reads any plain text (or markdown) from the input file, eg. */some/path/mynovel.md*
- writes the stylised converted text in the target *format* to the current directory, eg. as mynovel.doc
- target output *format* will be typically odt or doc required by a publisher. The *format* is passed to *pandoc* so you can try any other pandoc output formats
- changes all double and single "straight" 'computer' quotes to their properly stylised English or Czech equivalents
- assumes that all opening quotes are preceded by a white space or a newline
- note: single newlines are ignored by markdown, so they will disappear from the pandoc output. Apparently, this is a feature, not a bug.
- ´čárky´ around words are additionally changed to double arrows (reversed french) quotes by *quotes-cz* in the Czech version.
- two consecutive dashes (minus signs) are turned into a short en-dash (used between numbers).
- three dashes are turned into a longer em-dash (used in sentences).
- three dots are turned into an ellipsis (marking some  unfinished text). 
- some markdown editors might already do the last three substitutions for you, in which case no harm is done.

**Example invocation:** quotes-en mynovel.md doc

**Todo:** downgrading nested double quotes to singles. For now, explicitly deploy single quotes inside double ones, which is the correct author style anyway.

**Gotcha:** Do not mix English and Czech text. Just use the right shell script for each language separately and then concatenate their outputs, if you must.
