

# C++ compiler and flags
CPP := g++
CPP_FLAGS := -Wall -m64 -gdwarf-2 -std=c++17 -c

#	Assembler and flags
ASM := yasm
ASM_FLAGS := -f elf64 -gdwarf2

#	Linker and flags (we use g++ for hybrid programs)
#	Note that the flag "-z noexecstack" is new and now required in most cases.
LINKER := g++
LINKER_FLAGS := -Wall -m64 -gdwarf-2 -no-pie -z noexecstack


# Executable name
BIN_NAME := main
BIN := ./$(BIN_NAME)


# "Phony" target to run our program. "Phony" means the target
#	doesn't name an actual file/folder, but an action to take
#
# Notice we have a dependency here.
# The "build" target is a dependency of the "run" target.
# We denote this by adding the build target's name
#	to the right of the run target's colon
# This means that whenever we execute the "run" target,
#	the "build" target gets ran first.
# This makes sense because we would want to be sure
#	our executable is built before trying to launch
#	the program.
run:	build
	@echo "Running program!"
	$(BIN)
.PHONY: run


# Another "phony" target.
# Notice it depends on the executable $(BIN) being built
#	which will cause the target below to run.
# Notice also it doesn't actually do anything. This means
#	the "build" target is essentially an alias, or shortcut.
build:	$(BIN)
.PHONY: build


# A real (non-phony) target which names the executable
# Trace back up to the variables defined at the top of this file
#	and you'll see that $(BIN) just expands to ./my-program
# The job of this target is to build your entire program.
$(BIN):	driver.o hello.o
	$(LINKER) $(LINKER_FLAGS) *.so *.o -o "$@"


# Compile our driver module
driver.o:	driver.cpp
	$(CPP) $(CPP_FLAGS) "$<" -o "$@"


# Compile our hello module
hello.o:	hello.asm
	$(ASM) $(ASM_FLAGS) "$<" -o "$@"


# Clean up our repo (having object files laying around is messsy)
# Cleaning is also sometimes a good idea if you suspect the Makefile isn't 100% correct
#	or compilers aren't refreshing the object files
# (don't remove the shared object file, as you get that elsewhere and aren't actually compiling it)
clean:
	-rm *.o
	-rm $(BIN)
.PHONY: clean








