SRC_NAME=jq-1.6

CFLAGS  += -std=c99 -D_GNU_SOURCE

all: config_test
	$(MAKE) -C $(SRC_NAME)

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./configure \
		--disable-docs \
		--disable-valgrind \
		--without-oniguruma \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) ; \
	)

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) distclean ; \
	fi ; \
	rm -f config_done

romfs:
	$(STRIP) $(SRC_NAME)/jq
	$(ROMFSINST) $(SRC_NAME)/jq /usr/sbin/jq
