default: build

BUILD_TYPE?=Release

CMAKE_OPTIONS= -DCMAKE_BUILD_TYPE=$(BUILD_TYPE) \
        -DCMAKE_EXPORT_COMPILE_COMMANDS=1 \
		-DCMAKE_CXX_STANDARD=20

cmake:
	cmake -S .  -B Build ${CMAKE_OPTIONS}

build:
	@if [ ! -d Build ]; then \
		$(MAKE) cmake; \
	fi
	cmake --build Build

build-clean-first:
	cmake --build Build --clean-first


.PHONY: build
