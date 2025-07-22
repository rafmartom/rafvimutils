# rafvimutils

Cross project encapsulated vim utilities
This repository has as a reference LucHermitte's [lh-vim-lib](https://github.com/LucHermitte/lh-vim-lib).

It should allow you import these utilities in your own projects easily.

## Installation , sourcing it with your vim


```
Plug 'https://github.com/rafmartom/rafvimutils'
```

Test it


```
:call rafmartom#test_hi#main()
:call rafmartom#test_bye#main()
```

## Including it as a dependency in your project

If you want to add just a few number of functions for your own project, you can do it by writting a `makefile`
(change `RAFVIMUTILS_TARGET_PATH` accordingly)`

```
.PHONY: help fetch-deps clean-deps

help:
	@echo "Dependency Management:"
	@echo "  fetch-deps  - Download dependencies"
	@echo "  clean-deps  - Remove dependency artifacts"

## ----------------------------------------------------------------------------
# @section DEPENDENCY_MANAGEMENT

RAFVIMUTILS_SOURCE_PATH := autoload/rafmartom
RAFVIMUTILS_TARGET_PATH := $(RAFVIMUTILS_SOURCE_PATH)
RAFVIMUTILS_FILES := test_hi.vim test_bye.vim # Add more files here

RAFVIMUTILS_TARGETS := $(addprefix $(RAFVIMUTILS_TARGET_PATH)/,$(RAFVIMUTILS_FILES))


fetch-deps: $(RAFVIMUTILS_TARGETS)

$(RAFVIMUTILS_TARGET_PATH)/%.vim:
	@mkdir -p $(RAFVIMUTILS_TARGET_PATH)
	curl -L "https://raw.githubusercontent.com/rafmartom/rafvimutils/master/$(RAFVIMUTILS_SOURCE_PATH)/$*.vim" -o "$@"

clean-deps:
	rm -rf $(RAFVIMUTILS_TARGETS)


## EOF EOF EOF DEPENDENCY_MANAGEMENT
## ----------------------------------------------------------------------------
```

Remember to add this on your `.gitignore` again (change `RAFVIMUTILS_TARGET_PATH` accordingly)`

```
RAFVIMUTILS_TARGET_PATH="autoload/rafmartom"
echo "# rafvimutils dependency" >> ./.gitignore
echo "${RAFVIMUTILS_TARGET_PATH}" >> ./.gitignore
```
