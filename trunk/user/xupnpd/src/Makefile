LUA      = lua-5.1.4
#LUA      = lua-5.2.0
STATIC   = false
CFLAGS   += -O2 -Wall
CPPFLAGS += -O2 -fno-exceptions -fno-rtti -I$(LUA) -L$(LUA) -D_LARGEFILE64_SOURCE
SRC      = main.cpp soap.cpp mem.cpp mcast.cpp luaxlib.cpp luaxcore.cpp luajson.cpp luajson_parser.cpp
LUAMYCFLAGS = -DLUA_USE_LINUX

ifeq ($(STATIC),true)
CFLAGS+=-static
LUAMYCFLAGS+=-static
endif

embedded:
	make -C $(LUA) a MYCFLAGS='$(LUAMYCFLAGS)'
	$(CC) $(CFLAGS) -c -o md5.o md5c.c
	$(CC) $(CPPFLAGS) $(LDFLAGS) -DWITH_URANDOM -o xupnpd $(SRC) md5.o -llua -lm -ldl

clean:
	make -C $(LUA) clean
	rm -f $(LUA)/liblua.a
	rm -f md5.o
	rm -f xupnpd
