#==================================================================================================
# PROJECT: bs_call 
# FILE: Makefile
# DATE: 02/10/2017
# AUTHOR(S): Simon Heath <simon.heath@gmail.com>
# DESCRIPTION: Builds bs_call and dbSNP_idx
#==================================================================================================

# Definitions
ROOT_PATH=..
include Makefile.mk

PROG=bs_call dbSNP_idx

BS_CALL_SRC=bs_call.c genotype_model.c
DBSNP_SRC=dbSNP_idx.c dbSNP_compress.c dbSNP_utils.c

BS_CALL_INC=bs_call.h bs_call_options.h uthash.h
DBSNP_INC=dbSNP_idx.h dbSNP_compress.h dbSNP_utils.h uthash.h

BIN=$(addprefix $(FOLDER_BIN)/, $(PROG))
INC=


BS_CALL_LIBS:= $(LIBS) -lpthread

DBSNP_LIBS:=-lm
ifeq ($(HAVE_OPENMP),1)
BS_CALL_LIBS:=$(BS_CALL_LIBS) -fopenmp
endif
ifeq ($(HAVE_ZLIB),1)
BS_CALL_LIBS:=$(BS_CALL_LIBS) -lz
endif
ifeq ($(HAVE_BZLIB),1)
BS_CALL_LIBS:=$(BS_CALL_LIBS) -lbz2
endif
BS_CALL_OBJ = ${BS_CALL_SRC:.c=.o}
DBSNP_OBJ = ${DBSNP_SRC:.c=.o}

all: setup $(BIN)

$(FOLDER_BIN)/bs_call: CFLAGS= $(GENERAL_FLAGS) $(SUPPRESS_CHECKS) $(OPTIMIZATION_FLAGS) $(BS_CALL_INCLUDE_FLAGS)
$(FOLDER_BIN)/bs_call: $(BS_CALL_OBJ) $(addprefix $(FOLDER_INCLUDE)/, $(BS_CALL_INC))
	$(CC) $(CFLAGS)  -o $@ $(BS_CALL_OBJ) $(BS_CALL_LIB_PATH_FLAGS) $(BS_CALL_LIBS)

$(FOLDER_BIN)/dbSNP_idx: CFLAGS= $(GENERAL_FLAGS) $(OPTIMIZATION_FLAGS) $(DBSNP_INCLUDE_FLAGS)
$(FOLDER_BIN)/dbSNP_idx: $(DBSNP_OBJ) $(addprefix $(FOLDER_INCLUDE)/, $(DBSNP_INC))
	$(CC) $(CFLAGS)  -o $@ $(DBSNP_OBJ) $(DBSNP_LIB_PATH_FLAGS) $(DBSNP_LIBS)

setup:
	mkdir -p $(FOLDER_BIN)
	
clean: 
	rm -f $(BS_CALL_OBJ) $(DBSNP_OBJ) $(BIN) a.out *~

