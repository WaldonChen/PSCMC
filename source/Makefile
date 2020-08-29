CC      := cc
CFLAGS  := -O2 -I./src -I./include
LDFLAGS :=
LIBS    := -lm
PREFIX  := /usr/local

PUBLIC_HDRS = $(wildcard include/*.h)
PRIVATE_HDRS = $(wildcard src/*.h)

all: bin/cscheme bin/scmc2c_pre_pass bin/scmc2c_multi_pass

bin/cscheme: cscheme.o
	$(CC) $(LDFLAGS) $^ -o $@ $(LIBS)

bin/scmc2c_pre_pass: pre_passes.o hashcore_scmc.o
	$(CC) $(LDFLAGS) $^ -o $@ $(LIBS)

bin/scmc2c_multi_pass: fin_shell.o hashcore_scmc.o
	$(CC) $(LDFLAGS) $^ -o $@ $(LIBS)

cscheme.o: src/cscheme.c $(PUBLIC_HDRS)
hashcore_scmc.o: src/hashcore_scmc.c $(PRIVATE_HDRS)
fin_shell.o: src/fin_shell.c $(PRIVATE_HDRS)

%.o: src/%.c
	$(CC) $(CFLAGS) $< -c

clean:
	-rm -f *.o
