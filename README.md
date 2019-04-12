# Quotes
**(C) Libor Spacek, 2019**

Unix/Linux shell script utility to typeset quotation marks,  dashes and ellipses in proper English or Czech language styles and to convert plain text or markdown to most formats required by publishers.

### Motivation
Proper typesetting is a fiddly businness. This utility aims to avoid spending a lot of time and care on it, as with Latex  for example, or fiddling with hundreds of obscure buttons on word-processors. The problem is that certain common typographical elements like quotation marks and dashes are just not present on keyboard layouts or at least not in their correct forms.

The solution recommended to authors is to use *markdown* for easy, non-distracting  input. The straight 'computer quotes' and minus signs for dashes can be easily speed typed into the markdown file.

*Markdown*, being just plain text, lends itself equally well to  machine processing by standard *Unix/Linux* utilities, such as *sed* and *pandoc* used by *Quotes*.  This script replaces the easy 'computer' characters with the relevant  correct unicodes for the typographical elements and finally converts the document to doc, odt, html or other formats demanded by the publishers. 

The difficult part was using sed to determine, without complete parsing, which quote is the opening one and which is the closing. It is not foolproof. That is if you mess up the input with isolated or multiple quote marks, expect the gigo (garbage in, garbage out) principle to kick in. Actually, white space before an opening quote is all that this script looks for, thus it is very fast. All remaining quotes are treated as closing quotes. It works well in practice.

### Installation
- Requires  Unix/Linux type system with sed and pandoc installed. 
- Download the relevant script for your favourite language: `quotes` for English typographical rules or `uvozovky` for Czech rules. Make sure it is accessible (in your path) by placing it into a relevant bin directory and make it executable: `chmod u+x quotes`. Alternatively, simply run it from your current directory as `./quotes`... or `./uvozovky`...

### Usage Notes
	quotes filename format
	uvozovky filename format
- reads any plain text (or markdown) input file, eg. */some/path/mynovel.md*
- writes the stylised converted text in the target *format* to the current directory, using the same root filename, eg. as mynovel.doc
- the target output *format* will be typically odt or doc required by a publisher. The *format* is passed to *pandoc*. Example invocation: `quotes mynovel.md doc`  
You can try any other pandoc output formats. 
- sometimes you may just wish to do the typesetting but stay with the original file  format. Then directly overwrite the original with the typeset version like this: `quotes mynovel.md md`  
The script will make you a backup copy of the original file first, eg. mynovel.bak.

### Typesetting
- changes all "double" and 'single' straight computer quotes to their properly stylised English or Czech equivalents
- assumes that all opening quotes are preceded by a white space (or a newline)
- note: single newlines are deleted by *markdown*, so they will disappear from the pandoc output too. Apparently, this is a 'feature' of *markdown* and not a bug. To achieve an ordinary newline, you have to know 'the secret trick of two spaces'.
- ´čárky´ around words are additionally changed to double arrows »reversed french« quotes by *uvozovky* in the Czech version.
- two consecutive dashes -- (minus signs) are turned into a short en-dash (used between numbers).
- three dashes --- are turned into a longer em-dash (used in sentences).
- three dots ... are turned into ellipsis (marking some  unfinished text). 
- some markdown editors might do the last three substitutions for you, in which case no harm is done.

### Releases 
- **Apr 12 2019 Upgrade Release**  
added for safety automatic backing up when the original file is being overwritten  
added error message for wrong number of arguments  
the Czech version now has Czech language dialogues and has been renamed accordingly to "uvozovky"


**Todo:** downgrading nested double quotes to singles. For now, explicitly deploy single quotes inside double ones, which is the correct author style anyway.

**Gotcha:** Do not mix English and Czech texts, they have different typographical rules. Just use the right shell script for each language separately and then merge their outputs, if you must.

