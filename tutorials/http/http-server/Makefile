PROG ?= example                   # Program we are building
DELETE = rm -rf                   # Command to remove files
OUT ?= -o $(PROG)                 # Compiler argument for output file
SOURCES = main.c mongoose.c       # Source code files
CFLAGS = -W -Wall -Wextra -g -I.  # Build options
#CFLAGS += -fsanitize=address,undefined,alignment

# Mongoose build options. See https://mongoose.ws/documentation/#build-options
CFLAGS_MONGOOSE += -DMG_HTTP_DIRLIST_TIME_FMT="%Y/%m/%d %H:%M:%S"
CFLAGS_MONGOOSE += -DMG_ENABLE_LINES=1 -DMG_ENABLE_IPV6=1 -DMG_ENABLE_SSI=1
CFLAGS_EXTRA ?= -DMG_TLS=MG_TLS_BUILTIN

ifeq ($(OS),Windows_NT)   # Windows settings. Assume MinGW compiler. To use VC: make CC=cl CFLAGS=/MD OUT=/Feprog.exe
  PROG ?= example.exe           # Use .exe suffix for the binary
  CC = gcc                      # Use MinGW gcc compiler
  CFLAGS += -lws2_32 -lbcrypt   # Link against Winsock library
  DELETE = cmd /C del /Q /F /S  # Command prompt command to delete files
  OUT ?= -o $(PROG)             # Build output
endif

all: $(PROG)              # Default target. Build and run program
	$(RUN) ./$(PROG) $(ARGS)

$(PROG): $(SOURCES)       # Build program from sources
	$(CC) $(SOURCES) $(CFLAGS) $(CFLAGS_MONGOOSE) $(CFLAGS_EXTRA) $(OUT)

vc98:
	cl $(SOURCES) -DMG_ENABLE_SSI=1 -DMG_TLS=MG_TLS_BUILTIN

clean:                    # Cleanup. Delete built program and all build artifacts
	$(DELETE) $(PROG) *.o *.obj *.exe *.dSYM
