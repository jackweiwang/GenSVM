CC=gcc
CFLAGS=-Wall -O3 -g -rdynamic -DNDEBUG $(OPTFLAGS)
INCLUDE=-I../include/ -I./include
LIB=-L../lib

override LDFLAGS+=-lgensvm -lm

TEST_SRC=$(wildcard src/test_*.c)
TESTS=$(patsubst src/%.c,bin/%,$(TEST_SRC))

.PHONY: all

all: $(TESTS)
	bash ./runtests.sh

bin/%: src/%.c
	@echo $<
	@$(CC) $< -o $@ $(CFLAGS) $(INCLUDE) $(LIB) $(LDFLAGS)

valgrind:
	VALGRIND="valgrind --error-limit=no --leak-check=full \
		 --log-file=/tmp/valgrind-%p.log --track-origins=yes \
		 --show-leak-kinds=all -v" $(MAKE)

clean:
	rm -rf $(TESTS)
	rm -f ./tests.log
	rm -f /tmp/valgrind*.log