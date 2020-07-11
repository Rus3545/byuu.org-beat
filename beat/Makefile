include ../nall/Makefile
include ../phoenix/Makefile

application := beat
flags := $(flags) -std=gnu++11 -O3 -fomit-frame-pointer -I..
link := $(flags) -s
objects := obj/phoenix.o obj/$(application).o

rcflags = -o coff

ifeq ($(arch),i686)
rcflags += --target=pe-i386
out := out/32/
else
rcflags += --target=pe-x86-64
out := out/64/
endif


ifeq ($(platform),win)
  objects += obj/resource.o
endif

all: $(objects)
ifeq ($(platform),win)
endif
	$(compiler) -o $(out)$(application) $(objects) $(link) $(phoenixlink) -lX11

obj/resource.o:
	windres $(rcflags) ../phoenix/windows/phoenix.rc obj/resource.o

obj/phoenix.o:
	$(compiler) $(phoenixflags) -o obj/phoenix.o -c ../phoenix/phoenix.cpp

obj/$(application).o: $(application).cpp
	$(compiler) $(cppflags) $(flags) -o obj/$(application).o -c $(application).cpp

resource: force
	sourcery resource/resource.xml resource/resource.cpp resource/resource.hpp

install:
	sudo cp $(application) /usr/local/bin/$(application)

uninstall:
	sudo rm /usr/local/bin/$(application)

clean:
	-@$(call delete,obj/*.o)

force:
