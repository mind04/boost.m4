# Copyright (C) 2007  Benoit Sigoure <tsuna@lrde.epita.fr>
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

EXTRA_DIST = testsuite.at $(TESTSUITE) atlocal.in package.m4.in
TESTSUITE = $(srcdir)/testsuite
CLEANFILES = atconfig

check-local: atconfig atlocal $(TESTSUITE)
	$(SHELL) $(TESTSUITE) $(TESTSUITEFLAGS)

# Run the test suite on the *installed* tree (not necessary ATM => disabled).
#installcheck-local: atconfig atlocal $(TESTSUITE)
#	$(SHELL) $(TESTSUITE) AUTOTEST_PATH="$(bindir)" $(TESTSUITEFLAGS)

clean-local:
	test ! -f $(TESTSUITE) || $(SHELL) $(TESTSUITE) --clean
	rm -f -r autom4te.cache

AUTOTEST = $(AUTOM4TE) --language=autotest

$(TESTSUITE): $(srcdir)/package.m4.in $(srcdir)/testsuite.at
	$(AUTOTEST) -I '$(srcdir)' $@.at -o $@.tmp
	mv $@.tmp $@

atconfig: $(top_builddir)/config.status
	cd $(top_builddir) && $(SHELL) ./config.status tests/$@
