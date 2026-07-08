# njs

include $(dir $(abspath $(lastword $(MAKEFILE_LIST))))/version
NJS_URL := https://github.com/freeunitorg/njs/releases/download/$(NJS_VERSION)/njs-$(NJS_VERSION).tar.gz

PKGS += njs

$(TARBALLS)/njs-$(NJS_VERSION).tar.gz:
	$(call download_pkg,$(NJS_URL),njs)

.sum-njs: njs-$(NJS_VERSION).tar.gz

njs: njs-$(NJS_VERSION).tar.gz .sum-njs
	$(UNPACK)
	$(MOVE)

# njs 1.0.0 recommends QuickJS, but it is an external dependency.
.njs: njs
	cd $< && ./configure \
		--no-quickjs \
		--no-libxml2 \
		--no-zlib \
		&& $(MAKE) libnjs
	touch $@
