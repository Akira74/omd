include ../../Makefile.omd

NAME     = python-modules
VERSION  = $(OMD_VERSION)
DISTRO   = $(shell ../../distro)

# This is where the python modules are going to be installed to
LOCALPYTHONDIR=$(DESTDIR)$(OMD_ROOT)/lib/python

MODULES =

# Shinken
MODULES += setuptools-24.2.0.tar.gz
ifeq ($(shell ./python_greater_2.6.sh),0)
    MODULES += multiprocessing-2.6.2.1.tar.gz
endif
MODULES += simplejson-3.8.2.tar.gz
MODULES += pysphere-0.1.7.zip
MODULES += Pyro4-4.18.tar.gz
MODULES += pymongo-2.5.2.tar.gz
# end of shinken

MODULES += texttable-0.8.4.tar.gz
MODULES += ordereddict-1.1.tar.gz
MODULES += pyexcel-io-0.1.0.tar.gz
MODULES += pyexcel-0.2.0.tar.gz
MODULES += odfpy-0.9.6.tar.gz
MODULES += pyexcel-ods-0.1.0.tar.gz
MODULES += jdcal-1.2.tar.gz
MODULES += openpyxl-2.2.2.tar.gz
MODULES += importlib-1.0.3.zip
MODULES += argparse-1.4.0.tar.gz
MODULES += future-0.15.2.tar.gz
MODULES += xlwt-future-0.8.0.tar.gz
MODULES += xlrd-0.9.4.tar.gz
MODULES += pyexcel-xlsx-0.1.0.tar.gz
MODULES += pyexcel-xls-0.1.0.tar.gz
MODULES += MarkupSafe-0.23.tar.gz
MODULES += Jinja2-2.8.tar.gz
MODULES += wstools-0.4.tar.gz
MODULES += fpconst-0.7.2.tar.gz
MODULES += docutils-0.12.tar.gz
MODULES += SOAPpy-0.12.5.tar.gz
MODULES += PyYAML-3.10.tar.gz
MODULES += ecdsa-0.10.tar.gz
MODULES += gearman-2.0.2.tar.gz
MODULES += six-1.10.0.tar.gz
MODULES += orderedmultidict-0.7.5.tar.gz
MODULES += pyasn1-0.1.4.tar.gz
MODULES += pycrypto-2.6.1.tar.gz
MODULES += paramiko-1.12.2.tar.gz
MODULES += pysnmp-4.2.3.tar.gz
MODULES += pywbem-0.7.0.tar.gz
MODULES += requests-2.10.0.tar.gz

# More datasources for coshsh
MODULES += MySQL-python-1.2.5.zip
MODULES += pymssql-2.1.3.tar.gz

# DataScryer:
#MODULES += functools32-3.2.3-2.tar.gz
#MODULES += vcversioner-2.16.0.0.tar.gz
#MODULES += jsonschema-2.5.1.tar.gz


build:
	mkdir -p dest
	set -e ; cd dest && \
	    export PYTHONPATH=$$PYTHONPATH:$(LOCALPYTHONDIR); \
	    export PYMSSQL_BUILD_WITH_BUNDLED_FREETDS=1; \
	    for M in $(MODULES); do \
	        if echo $$M | grep .tar.gz; then \
	            tar xzf ../src/$$M ; \
	        else \
	            unzip -o ../src/$$M ; \
	        fi; \
	        MDIR=$$(echo $$M | sed -e 's/.tar.gz//g' -e 's/.zip//g') ; \
	        cd $$MDIR; \
	        echo PYTHONBUILD $$M ; \
	        python setup.py build ; \
	        cd .. ; \
	    done

install:
	mkdir -p $(LOCALPYTHONDIR)
	set -e ; cd dest && \
	    export PYTHONPATH=$$PYTHONPATH:$(LOCALPYTHONDIR); \
	    for M in $(MODULES); do \
	        MDIR=$$(echo $$M | sed -e 's/.tar.gz//g' -e 's/.zip//g') ; \
	        MNAME=$$(echo $$MDIR | sed -e 's/\-[0-9\.]*$//g' | tr 'A-Z' 'a-z' ) ; \
	        cd $$MDIR ; \
	        echo PYTHONINSTALL $$M ; \
	        python setup.py install --home=$(DESTDIR)$(OMD_ROOT) \
	            --prefix='' \
	            --install-platlib=$(LOCALPYTHONDIR) \
	            --install-purelib=$(LOCALPYTHONDIR) ; \
	        cd .. ; \
	    done

skel:

clean:
	rm -rf dest
