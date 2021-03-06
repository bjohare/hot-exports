#------------------------------------------------------------------------------
#
#  Makefile for Custom Data Export
#
#------------------------------------------------------------------------------

CXX = g++
#CXX = clang

CXXFLAGS = -O3
#CXXFLAGS = -g

#CXXFLAGS += -Wall -Wextra -Wredundant-decls -Wdisabled-optimization -pedantic -Wctor-dtor-privacy -Wnon-virtual-dtor -Woverloaded-virtual -Wsign-promo
#CXXFLAGS += -Wpadded -Winline -Weffc++ -Wold-style-cast

# uncomment this if you want information on how long it took to build the multipolygons
#CXXFLAGS += -DOSMIUM_WITH_MULTIPOLYGON_PROFILING

CXXFLAGS_GEOS    = -DOSMIUM_WITH_GEOS $(shell geos-config --cflags)
CXXFLAGS_SHAPE   = -DOSMIUM_WITH_SHPLIB $(CXXFLAGS_GEOS)
CXXFLAGS_LIBXML2 = -DOSMIUM_WITH_OUTPUT_OSM_XML $(shell xml2-config --cflags)
CXXFLAGS_OGR     = -DOSMIUM_WITH_OGR $(shell gdal-config --cflags)

CXXFLAGS += -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64


LDFLAGS = -L/usr/local/lib -lexpat -lpthread

LIB_SQLITE   = -lsqlite3
LIB_V8       = -lv8
LIB_GEOS     = $(shell geos-config --libs)
LIB_PROTOBUF = -lz -lprotobuf-lite -losmpbf
LIB_XML2     = $(shell xml2-config --libs)
LIB_OGR      = $(shell gdal-config --libs)

PROGRAMS = cde

.PHONY: all clean

all: $(PROGRAMS)

cde: cde.cpp
	$(CXX) $(CXXFLAGS) $(CXXFLAGS_OGR) $(CXXFLAGS_GEOS) -o $@ $< $(LDFLAGS) $(LIB_PROTOBUF) $(LIB_OGR) $(LIB_GEOS) -lboost_regex

clean:
	rm -f *.o core $(PROGRAMS)

