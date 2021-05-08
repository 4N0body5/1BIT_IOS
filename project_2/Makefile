SOURCE=proj2.c
PROJECT=proj2
OUTPUT=proj2.out

CC=gcc
CFLAGS=-std=gnu99 -Wall -Wextra -Werror -pedantic
LDFLAGS=-lrt -pthread

all:
	$(CC) $(CFLAGS) $(SOURCE) -o $(PROJECT) $(LDFLAGS)

run: all
	./$(PROJECT) 6 3 200 400

zip: clean
	zip $(PROJECT).zip $(SOURCE) Makefile

clean:
	rm -rf $(OUTPUT) $(PROJECT) $(PROJECT).zip

show:
	cat $(OUTPUT)
