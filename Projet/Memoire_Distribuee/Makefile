include Make_linux.inc
#include Make_msys2.inc
#include Make_osx.inc

CXXFLAGS = -std=c++14 -fPIC `sdl2-config --cflags`
ifdef DEBUG
CXXFLAGS += -g -O0 -Wall -fbounds-check -pedantic -D_GLIBCXX_DEBUG
else
CXXFLAGS += -O3 -march=native -Wall
endif

LIBS = $(LIB) `sdl2-config --cflags` `sdl2-config --libs` -lSDL2_image



ALL= colonisation.exe

default:	help

all: $(ALL)

clean:
	@rm -fr src/*.o *.exe src/*~ 

OBJS = src/galaxie.o src/parametres.o src/colonisation.o

src/galaxie.o:	src/galaxie.cpp src/galaxie.hpp
	$(CXX) $(CXXFLAGS) -c src/galaxie.cpp -o src/galaxie.o

src/parametres.o: src/parametres.cpp src/parametres.hpp src/galaxie.hpp
	$(CXX) $(CXXFLAGS) -c src/parametres.cpp -o src/parametres.o

src/colonisation.o: src/colonisation.cpp src/parametres.hpp src/galaxie.hpp
	$(CXX) $(CXXFLAGS) -c src/colonisation.cpp -o src/colonisation.o

colonisation.exe : $(OBJS)
	$(CXX) $(CXXFLAGS) $(OBJS) -o colonisation.exe $(LIBS)

help:
	@echo "Available targets : "
	@echo "    all            : compile the executable"
	@echo "    colonisation.exe     : compile the executable"
	@echo "Add DEBUG=yes to compile in debug"
	@echo "Configuration :"
	@echo "    CXX      :    $(CXX)"
	@echo "    CXXFLAGS :    $(CXXFLAGS)"

show:
	@echo "LIB   : $(LIB)"
	@echo "LIBS  : $(LIBS)"

%.html: %.md
	pandoc -s --toc $< --css=./github-pandoc.css -o $@
