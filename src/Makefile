#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      PLATFORM - Target platform: HOST or MSP432 (HOST if not specified)
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides
PLATFORM = HOST

ifeq ($(PLATFORM),MSP432)
	# Architectures Specific Flags for MSP432
	LINKER_FILE = MKL25Z128xxx4_flash.ld
	CPU = 
	ARCH = 
	SPECS = 

	# Compiler Flags and Defines for MSP432
	CC = arm-none-eabi-gcc
	LD = arm-none-eabi-ld
	LDFLAGS = 
	CFLAGS = 
	CPPFLAGS = 
else
        # Architectures Specific Flags for HOST
	LINKER_FILE =
	CPU =
	ARCH =
	SPECS =

	# Compiler Flags and Defines for HOST
	CC = gcc
	LD = ld
	LDFLAGS = -Wl,-Map=$(TARGET).map
	CFLAGS = -Wall -Werror -g -O0 -std=c99
	CPPFLAGS = -D$(PLATFORM)
endif

TARGET = c1m2
OBJS = $(SOURCES:.c=.o)

test:
	echo $(PLATFORM) $(CC) $(SOURCES) $(OBJS)

%.i : %.c
	$(CC) -E $< $(CFLAGS) $(CPPFLAGS) $(INCLUDES) -o $@

%.asm : %.c
	$(CC) -S $< $(CFLAGS) $(CPPFLAGS) $(INCLUDES) -o $@

%.o : %.c
	$(CC) -c $< $(CFLAGS) $(CPPFLAGS) $(INCLUDES) -o $@

.PHONY:compile-all
compile-all: $(OBJS)

.PHONY:build
build: $(TARGET).out

$(TARGET).out: $(OBJS)
	$(CC) $(OBJS) $(CFLAGS) $(LDFLAGS) -o $@

.PHONY: clean
clean:
	rm -f *.o *.i *.asm *.d $(TARGET).out $(TARGET).map
