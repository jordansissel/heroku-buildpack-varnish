site=http://err.no/tmp
version=3.0.3~pre20120523
package=varnish-$(version).tar.gz
workdir=$(CACHE_DIR)/varnish-$(version)

.PHONY: default
default: install

$(CACHE_DIR):
	mkdir $(CACHE_DIR)

$(CACHE_DIR)/$(package): | $(CACHE_DIR)
	wget -O $@ "$(site)/$(package)"

$(BUILD_DIR):
	mkdir $(BUILD_DIR)

$(workdir): $(CACHE_DIR)/$(package) | $(BUILD_DIR)
	tar -C $(dir $@) -zxf "$<"

.PHONY: configure
configure: | $(workdir)
	cd $(workdir); ./configure --prefix=$(BUILD_DIR) --without-rst2man --without-rst2html

.PHONY: compile
compile: | configure
	make -C $(workdir)

.PHONY: install
install: | compile
	make -C $(workdir) install
