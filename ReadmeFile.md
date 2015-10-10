## Introduction ##
This is just the README file from the source, with some markup.  **Note that this is from [revision 4](https://code.google.com/p/iso-14649-toolkit/source/detail?r=4), so it is somewhat outdated.  Here's the [latest version](http://code.google.com/p/iso-14649-toolkit/source/browse/trunk/iso-14649-toolkit/README).**

## OVERVIEW ##

---


This directory contains a C++ software toolkit built at NIST for programming with ISO 14649 Parts 10 and 11. Those parts are a data model to be used for control of a machining center. About three-quarters of Parts 10 and 11 are covered.

The toolkit contains four principal items (plus utilities).

  1. C++ class definitions and implementations.
  1. A parser for STEP Part 21 files.
  1. A simple stand-alone parser/printer.
  1. An ISO 14649 interpreter for 3-axis machining.

The software is all in standard C++, so it may be compiled and run on any computer for which a standard C++ compiler is available.


## C++ CLASSES ##

---


The C++ classes are covered by two files:

  1. iso14649classes.hh - This is a header file with class definitions that include implementations of constructors, access functions, and identifier functions. The class names and the names of attributes in the classes match the names given ISO 14649.
  1. iso14649classes.cc - This is a code file with implementations of destructors and STEP Part 21 file printers.

The C++ class files were generated automatically by a utility (sebnf2pars) built at NIST.


## PARSER ##

---


This is source code that may be compiled into an application. The parser builds a parse tree using the C++ classes.  It is a YACC-Lex parser.

The parser source code was also generated automatically by sebnf2pars.


## STAND-ALONE PARSER/PRINTER ##

---


The stand-alone parser/printer uses the parser to read and check a STEP Part 21 file, write the file back out again, and display the parse tree built by the parser. The executable is named iso14649parser.

The iso14649parser may be used two different ways.

> A. The iso14649parser may be used to parse one ISO 14649 Part 21 file corresponding to Parts 10 and 11 of ISO 14649. To use it that way, it should be called with one argument which is the path to the file, and the file must have a .stp suffix. For example: bin/iso14649parser data/ex1.stp. When the parser is used this way, it:
    1. reads and stores the contents of the file. If there are errors in parsing, an error message is printed for each error describing the error and printing the line of the input file that caused the error, up to the point at which the error occurred.
    1. prints the number of errors it found,
    1. prints the file out again, and
    1. if there were no errors, prints the skeleton of the parse tree that was created by parsing the file.
> B. The parser may also be used to parse many such files. To use it that way, it should be called with one argument which is the path to a file containing the paths to the files to parse, and the file must not have a .stp suffix. For example: _bin/iso14649parser data/filenames_ When the parser is used this way, for each input file it:
    1. prints the name of the file,
    1. reads and stores the contents of the file, printing error messages as described above, and
    1. prints the number of errors it found.


## INTERPRETER ##

---


This is an ISO 14649 interpreter for 3-axis machining. It reads STEP Part 21 files corresponding to the data model described in Parts 10 and 11 of ISO 14649 and interprets them. The output of the interpreter is calls to canonical machining commands.

This interpreter implements only a modest portion of Parts 10 and 11. Enough has been implemented to handle Example 1 in Annex E of Part 11 plus the equivalent of that example written using explicit toolpaths.

The interpreter includes toolpath generators for rough and finish plane milling, rough and finish rectangular pocket milling, drilling, multistep drilling, reaming, center drilling, countersinking, and counterboring.

Explicit toolpaths must consist of straight line segments, arcs of circles, and arcs of helixes.

The interpreter has a simple text-based user interface that should be self-explanatory. To start the interpreter, from the toolkit14649 directory, give the command: _bin/iso14649interp_

It is intended to be easy to modify the interpreter. Utilities are included that will automatically rebuild some of the secondary source code (iso14649\_err.c and iso14649\_err.h) if iso14649interp.cc is modified.


## DIRECTORY STRUCTURE ##

---


The top-level toolkit14649 directory has this README file, a Makefile and
five subdirectories:
  1. bin - executables, originally empty
  1. data - 2 test input files, 2 output files, and 2 tool files
  1. include - 5 header files
  1. ofiles - object files, originally empty
  1. source - mostly C++ source code, but also YACC and Lex files.


## COMPILING ##

---


If you have a Linux or Unix system, to compile everything, change the
the definitions of COMPILE and LINK in the Makefile to use your C++
compiler and give the following commands from the toolkit14649 directory:
make bin/iso14649parser
make bin/iso14649interp

**If you have a Windows system you are on your own.**