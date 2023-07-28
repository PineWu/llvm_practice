# This Makefile provides a template for building LLVM projects.

ifndef VERBOSE
QUIET := @
endif

SRC_IDR ?= $(shell pwd)

LLVM_CONFIG := llvm-config

COMMON_FLAGS = -Wall -Wextra

LDFLAGS += $(shell $(LLVM_CONFIG) --ldflags)
LDLIBS += $(shell $(LLVM_CONFIG) --libs core support bitreader bitwriter)
CXXFLAGS += $(COMMON_FLAGS) $(shell $(LLVM_CONFIG) --cxxflags)
CPPFLAGS += $(shell $(LLVM_CONFIG) --cppflags) -I$(SRC_DIR)

CXX := clang++
CC := clang

TARGET := helloworld
TARGET_OBJECTS := $(patsubst %.cpp,%.o,$(wildcard *.cpp))
SRC_FILES := $(wildcard *.cpp)

default: $(TARGET)

%.o : $(SRC_DIR)/%.cpp
	@echo Compiling $*.cpp
	$(QUIET) $(CXX) -c $(CPPFLAGS) $(CXXFLAGS) $<

$(TARGET) : $(TARGET_OBJECTS)
	@echo Linking $@
	$(QUIET) $(CXX) -o $@ $(CXXFLAGS) $(LDFLAGS) $^ $(LDLIBS)

print:
	@echo $(TARGET_OBJECTS)
	@echo $(SRC_FILES)
