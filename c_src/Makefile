NIF_SO = ../priv/libsecp256k1_nif.so
LIB_DIR = secp256k1
LIB_AR = $(LIB_DIR)/.libs/libsecp256k1.a

ERLANG_PATH = $(shell erl -eval 'io:format("~s", [lists:concat([code:root_dir(), "/erts-", erlang:system_info(version), "/include"])])' -s init stop -noshell)
CFLAGS += -I $(ERLANG_PATH) -I $(LIB_DIR) -I $(LIB_DIR)/src -I $(LIB_DIR)/include

ifneq ($(OS),Windows_NT)
	CFLAGS += -fPIC

	ifeq ($(shell uname),Darwin)
		LDFLAGS += -dynamiclib -undefined dynamic_lookup
	endif
endif

LDFLAGS += $(LIB_AR) -lgmp


.PHONY: clean

all: $(NIF_SO)

$(NIF_SO): libsecp256k1_nif.c $(LIB_AR)
	$(CC) $(CFLAGS) -shared -o $@ $< $(LDFLAGS)

$(LIB_AR): $(LIB_DIR)/Makefile
	$(MAKE) -C $(LIB_DIR)

$(LIB_DIR)/Makefile:
	cd $(LIB_DIR) && ./autogen.sh && ./configure --enable-module-recovery

clean: $(LIB_DIR)/Makefile
	$(MAKE) -C $(LIB_DIR) clean
	$(RM) $(NIF_SO)
