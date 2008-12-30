COMPILE = /usr/bin/g++ -c -v -g -Wall

LINK = /usr/bin/g++ -v

STEP_O = ofiles/iso14649YACC.o\
         ofiles/iso14649Lex.o\
         ofiles/iso14649classes.o

STEP_H = include/iso14649classes.hh\
         include/iso14649YACC.hh

INCLUDE = -Iinclude

bin/iso14649interp: ofiles/driver.o\
          ofiles/iso14649interp.o\
          ofiles/iso14649_err.o\
          ofiles/canon.o $(STEP_O)
	$(LINK) -o bin/iso14649interp\
                   ofiles/driver.o\
                   ofiles/iso14649interp.o\
                   ofiles/iso14649_err.o\
                   ofiles/canon.o $(STEP_O)

bin/iso14649parser: ofiles/iso14649parser.o $(STEP_O)
	$(LINK) -o bin/iso14649parser ofiles/iso14649parser.o $(STEP_O)

bin/lex_errors: source/lex_errors.lex
	flex -t source/lex_errors.lex > source/lex_errors.cc
	g++ -v -g -Wall -o bin/lex_errors source/lex_errors.cc

bin/write_err_array: source/write_err_array.c
	g++ -v -g -Wall -o bin/write_err_array source/write_err_array.c

bin/write_err_code: source/write_err_code.c
	g++ -v -g -Wall -o bin/write_err_code source/write_err_code.c

include/iso14649_err.h: source/iso14649interp.cc\
               bin/lex_errors\
               bin/write_err_code\
               bin/write_err_array
	bin/lex_errors < source/iso14649interp.cc > junk1
	sort -u junk1 > junk2
	bin/write_err_code < junk2 > include/iso14649_err.h
	bin/write_err_array < junk2 > source/iso14649_err.c
	rm junk1 junk2

ofiles/canon.o: source/canon.cc include/canon.hh
	$(COMPILE) $(INCLUDE) -o ofiles/canon.o source/canon.cc

ofiles/driver.o: source/driver.cc include/canon.hh include/iso14649interp.hh
	$(COMPILE) $(INCLUDE) -o ofiles/driver.o source/driver.cc

ofiles/iso14649classes.o: source/iso14649classes.cc\
                          include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649classes.o\
                                 source/iso14649classes.cc

ofiles/iso14649_err.o: source/iso14649_err.c include/iso14649_err.h
	$(COMPILE) -o ofiles/iso14649_err.o source/iso14649_err.c

ofiles/iso14649Lex.o : source/iso14649Lex.cc\
                       include/iso14649YACC.hh\
                       include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649Lex.o source/iso14649Lex.cc

ofiles/iso14649YACC.o : source/iso14649YACC.cc\
                        include/iso14649YACC.hh\
                        include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649YACC.o source/iso14649YACC.cc

ofiles/iso14649interp.o: source/iso14649interp.cc include/iso14649interp.hh\
                         include/iso14649_err.h $(STEP_H)
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649interp.o\
                                 source/iso14649interp.cc

ofiles/iso14649parser.o : source/iso14649parser.cc include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649parser.o\
                   source/iso14649parser.cc

source/iso14649Lex.cc : source/iso14649.lex
	flex -L -t source/iso14649.lex > source/iso14649Lex.cc

source/iso14649YACC.cc : source/iso14649.y
	bison -d -l -o source/iso14649YACC.cc source/iso14649.y
	mv source/iso14649YACC.hh include

source/iso14649YACC.hh : source/iso14649.y
	bison -d -l -o source/iso14649YACC.cc source/iso14649.y
	mv source/iso14649YACC.hh include

source/iso14649_err.c: source/iso14649interp.cc\
               bin/lex_errors\
               bin/write_err_code\
               bin/write_err_array
	bin/lex_errors < source/iso14649interp.cc > junk1
	sort -u junk1 > junk2
	bin/write_err_code < junk2 > include/iso14649_err.h
	bin/write_err_array < junk2 > source/iso14649_err.c
	rm junk1 junk2


