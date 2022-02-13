---
title: "My general Makefile"
date: 2022-01-03T20:21:00.000Z
categories:
  - blog
tags:
  - Makefile
published: true
---

When I write a program, I want to concentrate on the actual problem instead of wasting my time studying complex code management tools. I have learned to use these tools for different languages like _npm_ or _maven_ as I need them in my daily work. However, I never spent much time on the build mechanisms, which often resulted in even simple bugs costing me much time to fix. So I need a simple solution to manage my C code. As a result, I organize my C projects using a unified, minimal Makefile structure. The consistent Makefile structure helps me to quickly find my way around the code base and makes it easier to quickly adapt and extend my numerous projects. 

GNU **make** supports this approach: once you understand the principle, you can manage your code for building simple projects without losing control over it. In most cases, a handwritten Makefile is sufficient for minor or even large projects.

There are already many templates on the Internet for creating a proper Makefile. A helpful approach to creating a general Makefile is described in [Practical Makefiles, by example](http://nuclear.mutantstargoat.com/articles/make/).

Directory structures for build-folders, etc., are not used. As a result, the source code is mixed up with the build files. This can be tolerated as long as the number of source code files is kept as small as possible. If the project's complexity increases, it is more an indicator to split the project into smaller ones or tidy up.

Based on this template, I have created the structure of the Makefiles for all my projects, with a project-specific part and a general, static part. This way, the Makefile can be optimized centrally, and the static part can be replaced easily in existing projects if needed. 


## My Makefile

```Makefile
#=====================================================================
# Build, test and install the geisten neural network library
#
# Typing 'make help' will print the available make commands
#
#======================================================================

PROJECT_NAME = geisten  
PREFIX ?= /usr/local

MKDIR_P ?= mkdir -p
RM ?= rm

#--------------------------- Change the following variables to modify the project ----------------------------

SOURCE =
TESTS = test_geisten
DOCS = geisten.h

# CFLAGS ?= -I. -march=native -mtune=native -MP -Wall -Wextra -mavx -Wstrict-overflow -ffast-math -fsanitize=address -O3 -MMD
CFLAGS ?= -I. -mtune=native -MP -Wall -Wextra -Wstrict-overflow  -ffast-math -O -MMD -g2
LDFLAGS ?= -ffast-math

#--------------------------------------- DON'T change this (static) part ----------------------------------------

OBJ = $(SOURCE:.c=.o) $(addsuffix .o,$(TESTS))
DEP = $(OBJ:.o=.d)
DOCS_MD = $(DOCS:.h=.md)



options:
	@echo $(PROJECT_NAME) build options:
	@echo "CFLAGS   = ${CFLAGS}"
	@echo "LDFLAGS  = ${LDFLAGS}"
	@echo "CC       = ${CC}"

all: options test docs ## build all unit tests of the project

# compile the object files
%.o : %.c
	$(CC) $(CFLAGS) -c $< $(LIB_PATH) $(LIBS) -o $@ $(LDFLAGS)

# build the unit test
test_%: test_%.o
	$(CC) -o $@ $< $(LDFLAGS)
	@./$@ ||  (echo "Test $^ failed" && exit 1)

test: $(TESTS) ## run all test programs
	@echo "Success, all tests of project '$(PROJECT_NAME)' passed."


.PHONY: clean
# clean the build
clean:  ## cleanup - remove the target (test) files
	rm -f $(OBJ) $(DEP) $(TESTS) $(DOCS_MD)

.PHONY: install
install: $(PROJECT_NAME).h  ## install the target build to the target directory ('$(DESTDIR)$(PREFIX)/include')
	install $< $(DESTDIR)$(PREFIX)/include/


# ----------------- TOOLS ------------------------------------------

# Create a markdown library documentation from a C header file
%.md: %.h
	@$(MKDIR_P) $(dir $@)
	./xtract.awk $< > $@

docs: $(DOCS_MD) ## build the documentation of the header files in markdown format


# just type 'make print-VARIABLE to get the value of the variable >>VARIABLE<<
print-%  : ; @echo $* = $($*) ## get the value of a makefile variable '%' (type make print-VARIABLE to get value of VARIABLE)

.DEFAULT_GOAL=all

-include $(DEP)
```


## My little Makefile helpers

The description of a Makefile command is added via a comment. A double **##** helps awk to parse the Makefile for the help text when calling _make help_.

```Makefile
help: ## show this make help info
	@awk -F ':|##' '/^[^\t].+?:.*?##/ {\
		printf "\033[36m%-30s\033[0m %s\n", $$1, $$NF \
		}' $(MAKEFILE_LIST)
```

Sometimes it can be helpful to display the value of a variable. This can be done with the following addition:

```Makefile
print-%  : ; @echo $* = $($*) 
```

Type _make print-VARIABLE_ to get the value of the variable **VARIABLE**

To quickly find my way around my projects, even months later, I try to keep the projects as small as possible and break complex problems into as many smaller parts as possible. This approach is not new; it is part of the Unix philosophy and is a core design principle of many programming languages. From my experience, the best way to manage this complexity is to separate these submodules into single, executable programs instead of classes or packages. 

