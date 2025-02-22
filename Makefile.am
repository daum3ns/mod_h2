# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
SUBDIRS         = @BUILD_SUBDIRS@
DIST_SUBDIRS    = mod_http2

ACLOCAL_AMFLAGS = -I m4

EXTRA_DIST     = \
    test/unit \
    test/Makefile.in \
    test/Makefile.am \
	test/mod_h2test/mod_h2test.c \
	test/mod_h2test/mod_h2test.h \
	test/conf \
	test/data \
	test/htdocs \
	test/*.py \
	test/*.ini.in


dist_doc_DATA   = README README.md LICENSE

dist-hook:
	@rm -rf $(distdir)/test/unit/.deps \
            $(distdir)/test/unit/.py* \
            `find $(distdir) -name __pycache__` \
            `find $(distdir) -name .deps` \
            `find $(distdir) -name .libs` \
            `find $(distdir) -name .dirstamp` \
            `find $(distdir) -name .pytest_cache` \
            `find $(distdir) -name "*.o"`

.PHONY: test

test:
	$(MAKE) -C test/ test

loadtest:
	$(MAKE) -C test/ loadtest

clean-local:
	$(MAKE) -C test/ clean

docker-test:
	docker-compose build debian-sid
	docker-compose build archlinux
	docker-compose run debian-sid
	docker-compose run archlinux
