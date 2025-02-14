SHELL = /bin/sh

CC = gcc
CFLAGS = -Wall -Wextra -Werror -std=c11 -g -I/opt/homebrew/Cellar/check/0.15.2/include
LDFLAGS = -L/opt/homebrew/Cellar/check/0.15.2/lib -lcheck -lm -lncurses
SRC = brick_game/tetris/backend.c gui/cli/frontend.c brick_game.c
GCOV_FLAGS = --coverage -fprofile-arcs -ftest-coverage

OS_NAME = $(shell uname)

ifeq ($(OS_NAME),Linux)
OPEN = xdg-open
endif

ifeq ($(OS_NAME),Darwin)
OPEN = open
endif

.PHONY: all build/libtetris.a install uninstall test gcov_report dvi dist clang_format clang_check valgrind clean

all: clear install

build/libtetris.a: $(SRC)
	mkdir -p build
	$(CC) $(CFLAGS) -c $(SRC)
	ar rcs build/libtetris.a *.o
	mv *.o build

install: clean build/libtetris.a
	echo 0 > build/high_score.txt
	$(CC) $(CFLAGS) brick_game.c -Lbuild -ltetris $(LDFLAGS) -o build/tetris

run: clean install
	build/tetris

uninstall:
	rm -rf build

clean:
	rm -rf build gcov
	rm -f unit_test/unit_test unit_test/high_score.txt
	find dvi ! -name 'documentation.tex' -type f -exec rm -f {} +
	rm -f tetris.tar.gz

dvi:
	xelatex -output-directory=dvi dvi/documentation.tex

dist: install
	tar -czvf tetris.tar.gz Makefile brick_game gui unit_test brick_game.c brick_game.h

test: clean build/libtetris.a
	echo 0 > unit_test/high_score.txt
	$(CC) $(CFLAGS) unit_test/unit_test.c -Lbuild -ltetris $(LDFLAGS) -o unit_test/unit_test
	cd unit_test && ./unit_test

gcov_report: clean build/libtetris.a
	mkdir -p gcov
	echo 0 > gcov/high_score.txt
	$(CC) $(CFLAGS) $(GCOV_FLAGS) unit_test/unit_test.c brick_game/tetris/backend.c -Lbuild -ltetris $(LDFLAGS) -o gcov/gcov_test
	cd gcov && ./gcov_test
	lcov --capture --directory . --output-file gcov/coverage.info
	lcov --remove gcov/coverage.info '*unit_test/*' --output-file gcov/coverage.info
	genhtml -o gcov/report gcov/coverage.info
	#$(OPEN) gcov/report/brick_game/tetris/index.html

clang_format:
	cp ../materials/linters/.clang-format .clang-format
	clang-format -i *.c *.h
	clang-format -i brick_game/tetris/*.c brick_game/tetris/*.h
	clang-format -i gui/cli/*.c gui/cli/*.h
	clang-format -i unit_test/*.c unit_test/*.h
	rm -f .clang-format

clang_check:
	cp ../materials/linters/.clang-format .clang-format
	clang-format -n *.c *.h
	clang-format -n brick_game/tetris/*.c brick_game/tetris/*.h
	clang-format -n gui/cli/*.c gui/cli/*.h
	clang-format -n unit_test/*.c unit_test/*.h
	rm -f .clang-format

clear:
	clear