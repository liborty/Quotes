# Quotes
**(C) Libor Spacek, 2019**

Shell script utility to typeset various plain quotation marks,  en and em dashes and ellipses in any plain text (such as markdown) and to convert the result  to most other known formats. It follows the typographical rules for correct quotation marks in English (both up) and in Czech (down - up). 

### Motivation
Typesetting can be a fiddly business. This utility aims to avoid spending a lot of time and care on it, as with Latex for example, or fiddling with hundreds of obscure buttons on commercial word-processors. The problem is that certain basic  typographical elements, like up / down / opening / closing quotation marks, dashes and ellipses are represented by uncommon single characters that are usually not present on keyboard layouts.  Even if somehow found or memorised, it is an unnecessary and error prone delay for an author to have to worry about choosing the right one (e.g. opening versus closing quotation marks).
  
The objective of this project is to facilitate easy and fast typing in plain (markdown) text, which is something that many authors will welcome. Invoking this simple shell script will then "magically"  turn the draft  into professional looking typeset result and also convert it from compact plaintext draft to any bloat-format required by backward publishers.

The solution recommended to authors is to use a *markdown*  editor, such as Ghostwriter, for easy, non-distracting  input. The straight 'computer quotes' and minus signs for dashes can be easily speed typed into the markdown draft.

*Markdown*, being just plain text, lends itself well to  machine processing by standard *Unix/Linux* utilities, such as *sed* and *pandoc*, as used by *Quotes*.  This script replaces the easy 'computer' characters with the relevant  correct unicodes for the typographical elements and optionally converts the final draft to doc, odt, html or other formats demanded by the publishers. 

The difficult part was using sed to determine, without complete parsing, which quote is the opening one and which is the closing. It is not foolproof. That is if you mess up the input with isolated or multiple quotation marks, expect the gigo (garbage in, garbage out) principle to kick in. Actually, white space before an opening quote is all that this script looks for, thus it is very fast. All remaining quotes are treated as closing quotes. It works well in practice, as long as you don't put spurious spaces before closing quotes.

### Installation
- Dependencies: requires  Unix/Linux type system with sed and pandoc installed. 
- Download the relevant script for your favourite language: `quotes` for English typographical rules or `uvozovky` for Czech rules. Make sure they are accessible (in your path) by placing them into a relevant bin directory and make them executable: `chmod u+x quotes uvozovky`. Alternatively, simply run them from your current directory as `./quotes`... or `./uvozovky`...

### Usage Notes
	quotes filename format
	uvozovky filename format
- reads any plain text (or markdown) input file, eg. */some/path/mynovel.md*
- writes the typeset text in the target *format* to the current directory, using the same root filename, eg. as mynovel.doc
- the target output *format* will be typically odt or doc required by a publisher. The *format* is passed to *pandoc*. Example invocation: `quotes mynovel.md doc`  
You can try any other pandoc output formats. 
- sometimes you may just wish to do the typesetting but stay with the original file  format. Then you can directly overwrite the original with the typeset version like this: `quotes mynovel.md md`  
The script will make you a backup copy of the original file first, eg. mynovel.bak.

### Typesetting
- changes all "double" and 'single' straight computer quotes to their properly stylised English or Czech equivalents
- assumes that all opening quotes are preceded by a white space (or a newline) and the closing ones are not
- note: single newlines are deleted by *markdown*, so they will disappear from the pandoc output too. Apparently, this is a 'feature' of *markdown* and not a bug. To achieve an ordinary newline, you have to know 'the secret trick of two spaces'.
- ´čárky´ (accents) around words are additionally changed to double arrows or »reversed french chevron quotes« by *uvozovky* , the Czech version.
- two consecutive dashes -- (minus signs) are turned into a short en-dash (used between numbers).
- three dashes --- are turned into a longer em-dash (used in sentences).
- three dots ... are turned into ellipsis (marking some  unfinished text). 
- some markdown editors might do some of the substitutions for you, in which case no harm is done.

### Releases 
- **Apr 13 2019** updated this README file  
- **Apr 12 2019 Upgrade Release**  
- added for safety automatic backing up when the original file is being overwritten  
- added error message for wrong number of arguments  
- the Czech version now has Czech language dialogues and has been renamed accordingly to "uvozovky"


**Todo:** downgrading nested double quotes to singles. For now, explicitly deploy single quotes inside double ones, which is the correct author style anyway.

**Gotcha:** Do not mix English and Czech texts, they have different typographical rules. Just use the right shell script for each language separately and then merge their outputs, if you must.

