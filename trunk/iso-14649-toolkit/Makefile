COMPILE = /usr/bin/g++ -c -v -g -Wall
LINK = /usr/bin/g++ -v
INCLUDE = -Iinclude

##################################################################

# making executables

bin/directify: source/directifyLex.cc
	 g++ -v -g -Wall -o bin/directify  source/directifyLex.cc

bin/iso14649interp: ofiles/driver.o\
                    ofiles/iso14649interp.o\
                    ofiles/iso14649_err.o\
                    ofiles/canon.o\
                    ofiles/iso14649YACC.o\
                    ofiles/iso14649Lex.o\
                    ofiles/iso14649classes.o
	$(LINK) -o bin/iso14649interp ofiles/driver.o\
                                      ofiles/iso14649interp.o\
                                      ofiles/iso14649_err.o\
                                      ofiles/canon.o\
                                      ofiles/iso14649YACC.o\
                                      ofiles/iso14649Lex.o\
                                      ofiles/iso14649classes.o

bin/iso14649parser : ofiles/iso14649YACC.o\
                     ofiles/iso14649Lex.o\
                     ofiles/iso14649classes.o\
                     ofiles/iso14649parser.o
	$(LINK) -o bin/iso14649parser ofiles/iso14649parser.o\
                                      ofiles/iso14649YACC.o\
                                      ofiles/iso14649Lex.o\
                                      ofiles/iso14649classes.o

bin/iso14649parserDirect : ofiles/iso14649YACCDirect.o\
                     ofiles/iso14649LexDirect.o\
                     ofiles/iso14649classesDirect.o\
                     ofiles/iso14649parserDirect.o
	$(LINK) -o bin/iso14649parserDirect ofiles/iso14649parserDirect.o\
                                            ofiles/iso14649YACCDirect.o\
                                            ofiles/iso14649LexDirect.o\
                                            ofiles/iso14649classesDirect.o

bin/lex_errors: source/lex_errors.lex
	flex -t source/lex_errors.lex > source/lex_errors.cc
	g++ -v -g -Wall -o bin/lex_errors source/lex_errors.cc

bin/write_err_array: source/write_err_array.c
	g++ -v -g -Wall -o bin/write_err_array source/write_err_array.c

bin/write_err_code: source/write_err_code.c
	g++ -v -g -Wall -o bin/write_err_code source/write_err_code.c



##################################################################

# making object files from .cc files

ofiles/canon.o: source/canon.cc include/canon.hh
	$(COMPILE) $(INCLUDE) -o ofiles/canon.o source/canon.cc

ofiles/driver.o: source/driver.cc include/canon.hh\
                                  include/iso14649interp.hh\
                                  include/iso14649_err.h
	$(COMPILE) $(INCLUDE) -o ofiles/driver.o source/driver.cc

ofiles/iso14649classes.o: source/iso14649classes.cc\
                          include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649classes.o\
                                 source/iso14649classes.cc

ofiles/iso14649classesDirect.o: source/iso14649classesDirect.cc\
                          include/iso14649classesDirect.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649classesDirect.o\
                                 source/iso14649classesDirect.cc

ofiles/iso14649interp.o: source/iso14649interp.cc include/iso14649interp.hh\
                         include/iso14649_err.h $(STEP_H)
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649interp.o\
                                 source/iso14649interp.cc

ofiles/iso14649Lex.o : source/iso14649Lex.cc\
                       include/iso14649YACC.hh\
                       include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649Lex.o\
                                 source/iso14649Lex.cc

ofiles/iso14649LexDirect.o : source/iso14649LexDirect.cc\
                       include/iso14649YACCDirect.hh\
                       include/iso14649classesDirect.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649LexDirect.o\
                                 source/iso14649LexDirect.cc

ofiles/iso14649parser.o : source/iso14649parser.cc\
                          source/iso14649classes.cc\
                          include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649parser.o\
                   source/iso14649parser.cc

ofiles/iso14649parserDirect.o : source/iso14649parserDirect.cc\
                          source/iso14649classesDirect.cc\
                          include/iso14649classesDirect.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649parserDirect.o\
                   source/iso14649parserDirect.cc

ofiles/iso14649YACC.o : source/iso14649YACC.cc\
                        include/iso14649YACC.hh\
                        include/iso14649classes.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649YACC.o\
                                 source/iso14649YACC.cc

ofiles/iso14649YACCDirect.o : source/iso14649YACCDirect.cc\
                        include/iso14649YACCDirect.hh\
                        include/iso14649classesDirect.hh
	$(COMPILE) $(INCLUDE) -o ofiles/iso14649YACCDirect.o\
                                 source/iso14649YACCDirect.cc

ofiles/iso14649_err.o: source/iso14649_err.c include/iso14649_err.h
	$(COMPILE) -o ofiles/iso14649_err.o source/iso14649_err.c

##################################################################

# making .cc files from YACC and lex files

source/directifyLex.cc : source/directify.lex
	flex -L -t source/directify.lex > source/directifyLex.cc

source/iso14649Lex.cc : source/iso14649.lex
	flex -L -t source/iso14649.lex > source/iso14649Lex.cc

source/iso14649LexDirect.cc : source/iso14649Direct.lex
	flex -L -t source/iso14649Direct.lex > source/iso14649LexDirect.cc

source/iso14649YACC.cc : source/iso14649.y
	bison -d -l -o source/iso14649YACC.cc source/iso14649.y
	mv source/iso14649YACC.hh include

source/iso14649YACCDirect.cc : source/iso14649Direct.y
	bison -d -l -o source/iso14649YACCDirect.cc source/iso14649Direct.y
	mv source/iso14649YACCDirect.hh include

source/iso14649YACC.hh : source/iso14649.y
	bison -d -l -o source/iso14649YACC.cc source/iso14649.y
	mv source/iso14649YACC.hh include

source/iso14649YACCDirect.hh : source/iso14649Direct.y
	bison -d -l -o source/iso14649YACCDirect.cc source/iso14649Direct.y
	mv source/iso14649YACCDirect.hh include

##################################################################

# making iso14649_err.c and iso14649_err.hh from iso14649interp.cc

source/iso14649_err.c: source/iso14649interp.cc\
               bin/lex_errors\
               bin/write_err_code\
               bin/write_err_array
	bin/lex_errors < source/iso14649interp.cc > junk1
	sort -u junk1 > junk2
	bin/write_err_code < junk2 > include/iso14649_err.h
	bin/write_err_array < junk2 > source/iso14649_err.c
	rm junk1 junk2

include/iso14649_err.h: source/iso14649interp.cc\
               bin/lex_errors\
               bin/write_err_code\
               bin/write_err_array
	bin/lex_errors < source/iso14649interp.cc > junk1
	sort -u junk1 > junk2
	bin/write_err_code < junk2 > include/iso14649_err.h
	bin/write_err_array < junk2 > source/iso14649_err.c
	rm junk1 junk2


##################################################################

#making iso14649parserDirect.cc from iso14649parser.cc

source/iso14649parserDirect.cc: source/iso14649parser.cc bin/directify
	bin/directify < source/iso14649parser.cc >\
                        source/iso14649parserDirect.cc
