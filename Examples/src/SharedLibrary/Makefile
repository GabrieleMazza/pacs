############################################################
#
# An example of Makefile for the course on 
# Advanced Programming for Scientific Computing
# It should be modified for adapting it to the various examples
#
############################################################
#
# The environmental variable PACS_ROOT should be set to the
# root directory where the examples reside. In practice, the directory
# where this file is found. The resolution of PACS_ROOT is made in the
# Makefile.h file, where other important variables are also set.
# The only user defined variable that must be set in this file is
# the one indicating where Makefile.h resides

MAKEFILEH_DIR=../../
#
include $(MAKEFILEH_DIR)/Makefile.inc
#
# You may have an include file also in the current directory
#
-include Makefile.inc

#
# The general setting is as follows:
# mains are identified bt main_XX.cpp
# all other files are XX.cpp
#

# get all files *.cpp
SRCS=$(wildcard *.cpp)
# get the corresponding object file
OBJS = $(SRCS:.cpp=.o)
# get all headers in the working directory
HEADERS=$(wildcard *.hpp)
#
exe_sources=$(filter main%.cpp,$(SRCS))
EXEC=$(exe_sources:.cpp=)

#========================== ORA LA DEFINIZIONE DEGLI OBIETTIVI
.phony= all clean distclean doc

.DEFAULT_GOAL = all

all: lib0 $(EXEC)

lib0:
	$(CXX) -Wall -O3 -fPIC -c smalllib.cpp
	$(CXX) -shared -Wl,-soname,libsmall.so.1 -o libsmall.so.1.0 smalllib.o
	ln -f -s libsmall.so.1.0 libsmall.so
	ln -f -s libsmall.so.1.0 libsmall.so.1
	rm -f smalllib.o
lib1:
	$(CXX) -Wall -fPIC -c smalllib2.cpp
	$(CXX) -shared -Wl,-soname,libsmall.so.1 -o libsmall.so.1.1 smalllib2.o
	ln -f -s libsmall.so.1.1 libsmall.so
	ln -f -s libsmall.so.1.1 libsmall.so.1
	rm -f smalllib2.o

main.o: main.cpp
	$(CXX) $(CXXFLAGS) -c -O3 -Wall main.cpp -o main.o

main: main.o
	$(CXX) $(LDFLAGS) $(LOADLIBES) main.o  -L. -lsmall -o main

development:
	$(MAKE) main LOADLIBES=-Wl,-rpath=.

clean:
	\rm -f *.o main libsmall.so lib*.so.* 

distclean:
	$(MAKE) clean
	-\rm -r -f ./doc
	-\rm -f *.out *.bak *~ $(DEPEND)

doc:
	doxygen $(DOXYFILE)

$(OBJS): $(SRCS)

$(DEPEND): $(SRCS) $(HEADERS)
	g++ $(CPPFLAGS) -MM $(SRCS) -MF $(DEPEND)



-include $(DEPEND)





