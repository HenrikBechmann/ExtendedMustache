# ExtendedMustache

This is an extended syntax of mustache that I wrote a long time ago.

The main interest is probably the conciseness of the parser, just over 500 lines, in PHP.

From the source code:

```

This is an implementation and extension of the mustache design pattern: 
		http://mustache.github.com/mustache.5.html
Basically: 
{{...}} connotes a variable (no closing tag, escaped; {{&...}} is unescaped) eg. {{totalsales}}
{{#...}} connotes a section (with a closing tag - {{/#...}}) eg. {{#recordset}}...{{/#recordset}}
General form {{<symbols>index}} ... {{/<symbols>index}}
variables do not require closing tag
indexes must start with alpha character and be followed by word characters (letters, digits, "_")
sections can be thought of as nested namespaces
delimiters:
{{...}} these cannot be changed (but it wouldn't be hard to extend the class to allow alternate delimiters)
symbols:
section qualifier:
#
alternate qualifier:
^ = inversion (IS NOT - replaces #)
additional qualifiers: 
& = unescaped variable
? = assertion (IS) for var, #
* = global (root dictionary) for var, #, ?, ^
specialized:
> = partial (template fragment)
! = comment (thrown away)
reserved:
+ = subsection (template recursion - reserved - not implemented)
Markup:
	Notes:
		* = global = reference to dictionary root associative array
		alternate, simpler, element closing tags are DEPRECATED, but available for MUSTACHE compatibility
assertions:	
	{{?*...}} ... {{/?*...}} or {{/...}}		global var assertion: exists, and true or not empty or numeric (0)
	{{?...}} ... {{/?...}} or {{/...}} 			var assertion: exists, and true or not empty or numeric (0)
	{{#?*...}} ... {{/#?*...}} or {{/?...}}		global section assertion: exists, and true or not empty or numeric (0)
	{{#?...}} ... {{/#?...}} or {{/?...}}		section assertion: exists, and true or not empty or numeric (0)
namespaces (nested sections):
	{{#*...}} ... {{/#*...}} or {{/...}}		global section
	{{#...}} ... {{/#...}} or {{/...}}			section: own scope of object or array, or variable assertion
inversions:
	{{^*...}} ... {{/^*...}} or {{/...}}		global inverted section or variable: doesn't exist, or false, or empty and not numeric (0)
	{{^...}} ... {{/^...}} or {{/...}}			inverted section or variable: doesn't exist, or false, or empty and not numeric (0)
specialized:
	{{>...}}									partial template: index taken as file name unless dictionary entry is set
	{{!...}}									comment: thrown away
variables:
	{{&*...}}									unescaped global var: no htmlspecialchar filter
	{{*...}}									global var: htmlspecialchar filter
	{{&...}}									unescaped var: no htmlspecialchar filter
	{{...}}										var: htmlspecialchar filter
	
template is combined with dictionary through markup.
dictionary: 
	root must be associative array
	nested values can be 
		basic datatypes, or 
		simple objects (interpreted as nested namespaces, converted to associative arrays)
		list arrays, which are iterated with parallel section template fragment
		list arrays must contain associative arrays or simple objects
template fragments and dictionary are processed and recursed in tandem
Template does not support function data type: preprocess dictionary instead.

```
