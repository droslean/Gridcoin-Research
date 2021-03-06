# Copyright (c) 2013-2016 The Bitcoin Core developers
# Distributed under the MIT software license, see the accompanying
# file COPYING or http://www.opensource.org/licenses/mit-license.php.

DIST_SUBDIRS = univalue

AM_LDFLAGS = $(PTHREAD_CFLAGS) $(LIBTOOL_LDFLAGS) $(HARDENED_LDFLAGS)
AM_CXXFLAGS = $(HARDENED_CXXFLAGS) $(ERROR_CXXFLAGS)
AM_CPPFLAGS = $(HARDENED_CPPFLAGS) -DSTATICLIB -DMINIUPNP_STATICLIB
EXTRA_LIBRARIES =

if EMBEDDED_UNIVALUE
LIBUNIVALUE = univalue/libunivalue.la

$(LIBUNIVALUE): $(wildcard univalue/lib/*) $(wildcard univalue/include/*)
	$(AM_V_at)$(MAKE) $(AM_MAKEFLAGS) -C $(@D) $(@F)
else
LIBUNIVALUE = $(UNIVALUE_LIBS)
endif

GRIDCOIN_CONFIG_INCLUDES=-I$(builddir)/config
GRIDCOIN_INCLUDES=-I$(builddir) -I$(builddir)/obj $(BDB_CPPFLAGS) $(BOOST_CPPFLAGS) $(LEVELDB_CPPFLAGS) $(CRYPTO_CFLAGS) $(SSL_CFLAGS) $(UNIVALUE_CFLAGS)

LIBGRIDCOIN_UTIL=libgridcoin_util.a
LIBGRIDCOINQT=qt/libgridcoinqt.a
LIBGRIDCOIN_CRYPTO_BASE=crypto/libgridcoin_crypto_base.a

LIBGRIDCOIN_CRYPTO= $(LIBGRIDCOIN_CRYPTO_BASE)
if ENABLE_SSE41
LIBGRIDCOIN_CRYPTO_SSE41 = crypto/libgridcoin_crypto_sse41.a
LIBGRIDCOIN_CRYPTO += $(LIBGRIDCOIN_CRYPTO_SSE41)
endif
if ENABLE_AVX2
LIBGRIDCOIN_CRYPTO_AVX2 = crypto/libgridcoin_crypto_avx2.a
LIBGRIDCOIN_CRYPTO += $(LIBGRIDCOIN_CRYPTO_AVX2)
endif

# Make is not made aware of per-object dependencies to avoid limiting building parallelization
# But to build the less dependent modules first, we manually select their order here:
EXTRA_LIBRARIES += $(LIBGRIDCOIN_UTIL) \
                   $(LIBGRIDCOIN_CRYPTO)


bin_PROGRAMS =
noinst_PROGRAMS =
TESTS =
BENCHMARKS =

if BUILD_GRIDCOINRESEARCHD
    bin_PROGRAMS += gridcoinresearchd
endif

.PHONY: FORCE
# gridcoin core #
GRIDCOIN_CORE_H = \
	addrman.h \
	alert.h \
	allocators.h \
	appcache.h \
	backup.h \
	base58.h \
	beacon.h \
	bignum.h \
	block.h \
	boinc.h \
	checkpoints.h \
	coincontrol.h \
	compat.h \
	compat/byteswap.h \
	compat/endian.h \
	contract/polls.h \
	contract/contract.h \
	cpid.h \
	crypter.h \
	db.h \
	fwd.h \
	global_objects.hpp \
	global_objects_noui.hpp \
	gridcoin.h \
	hash.h \
	init.h \
	kernel.h \
	key.h \
	keystore.h \
	main.h \
	miner.h \
	mruset.h \
	neuralnet.h \
	netbase.h \
	net.h \
	pbkdf2.h \
	prevector.h \
	protocol.h \
	rpcclient.h \
	rpcprotocol.h \
	rpcserver.h \
	script.h \
	scrypt.h \
	serialize.h \
	strlcpy.h \
	sync.h \
	tally.h \
	threadsafety.h \
	tinyformat.h \
	txdb.h \
	txdb-leveldb.h \
	ui_interface.h \
	uint256.h \
	util.h \
	version.h \
	walletdb.h \
	wallet.h

GRIDCOIN_CORE_CPP = addrman.cpp \
	alert.cpp \
	allocators.cpp \
	appcache.cpp \
	backup.cpp \
	beacon.cpp \
	block.cpp \
	boinc.cpp \
	checkpoints.cpp \
	contract/polls.cpp \
	contract/contract.cpp \
	cpid.cpp \
	crypter.cpp \
	db.cpp \
	gridcoin.cpp \
	init.cpp \
	kernel.cpp \
	key.cpp \
	keystore.cpp \
	main.cpp \
	miner.cpp \
	netbase.cpp \
	net.cpp \
	noui.cpp \
	pbkdf2.cpp \
	protocol.cpp \
	contract/rpccontract.cpp \
	rpcblockchain.cpp \
	rpcclient.cpp \
	rpcdump.cpp \
	rpcmining.cpp \
	rpcnet.cpp \
	rpcprotocol.cpp \
	rpcrawtransaction.cpp \
	rpcserver.cpp \
	rpcwallet.cpp \
	rpcdataacq.cpp \
	script.cpp \
	scrypt.cpp \
	sync.cpp \
	tally.cpp \
	txdb-leveldb.cpp \
	util.cpp \
	version.cpp \
	wallet.cpp \
	walletdb.cpp


obj/build.h: FORCE
	@$(MKDIR_P) $(builddir)/obj
	@$(top_srcdir)/share/genbuild.sh "$(abs_top_builddir)/src/obj/build.h" \
	  "$(abs_top_srcdir)"
libgridcoin_util_a-version.$(OBJEXT): obj/build.h

# util: shared between all executables.
# This library *must* be included to make sure that the glibc
# backward-compatibility objects and their sanity checks are linked.
libgridcoin_util_a_CPPFLAGS = $(AM_CPPFLAGS) $(GRIDCOIN_INCLUDES)
libgridcoin_util_a_CXXFLAGS = $(AM_CXXFLAGS) $(PIE_FLAGS)
libgridcoin_util_a_SOURCES = $(GRIDCOIN_CORE_CPP) \
    neuralnet_stub.cpp \
    $(GRIDCOIN_CORE_H)

if TARGET_WINDOWS
libgridcoin_util_a_CXXFLAGS += -DUNICODE
endif

nodist_libgridcoin_util_a_SOURCES = $(srcdir)/obj/build.h


# crypto primitives library
crypto_libgridcoin_crypto_base_a_CPPFLAGS = $(AM_CPPFLAGS)
crypto_libgridcoin_crypto_base_a_CXXFLAGS = $(AM_CXXFLAGS) $(PIE_FLAGS)
crypto_libgridcoin_crypto_base_a_SOURCES = \
  crypto/aes.cpp \
  crypto/aes.h \
  crypto/chacha20.h \
  crypto/chacha20.cpp \
  crypto/common.h \
  crypto/hmac_sha256.cpp \
  crypto/hmac_sha256.h \
  crypto/hmac_sha512.cpp \
  crypto/hmac_sha512.h \
  crypto/ripemd160.cpp \
  crypto/ripemd160.h \
  crypto/sha1.cpp \
  crypto/sha1.h \
  crypto/sha256.cpp \
  crypto/sha256.h \
  crypto/sha512.cpp \
  crypto/sha512.h

if USE_ASM
crypto_libgridcoin_crypto_base_a_SOURCES += crypto/sha256_sse4.cpp
endif

crypto_libgridcoin_crypto_sse41_a_CXXFLAGS = $(AM_CXXFLAGS) $(PIE_FLAGS)
crypto_libgridcoin_crypto_sse41_a_CPPFLAGS = $(AM_CPPFLAGS)
crypto_libgridcoin_crypto_sse41_a_CXXFLAGS += $(SSE41_CXXFLAGS)
crypto_libgridcoin_crypto_sse41_a_CPPFLAGS += -DENABLE_SSE41
crypto_libgridcoin_crypto_sse41_a_SOURCES = crypto/sha256_sse41.cpp

crypto_libgridcoin_crypto_avx2_a_CXXFLAGS = $(AM_CXXFLAGS) $(PIE_FLAGS)
crypto_libgridcoin_crypto_avx2_a_CPPFLAGS = $(AM_CPPFLAGS)
crypto_libgridcoin_crypto_avx2_a_CXXFLAGS += $(AVX2_CXXFLAGS)
crypto_libgridcoin_crypto_avx2_a_CPPFLAGS += -DENABLE_AVX2
crypto_libgridcoin_crypto_avx2_a_SOURCES = crypto/sha256_avx2.cpp

CTAES_DIST =  crypto/ctaes/bench.c
CTAES_DIST += crypto/ctaes/ctaes.c
CTAES_DIST += crypto/ctaes/ctaes.h
CTAES_DIST += crypto/ctaes/README.md
CTAES_DIST += crypto/ctaes/test.c

# gridcoinresearchd binary #
gridcoinresearchd_SOURCES = gridcoinresearchd.cpp
gridcoinresearchd_CPPFLAGS = $(AM_CPPFLAGS) $(GRIDCOIN_INCLUDES)
gridcoinresearchd_CXXFLAGS = $(AM_CXXFLAGS) $(PIE_FLAGS)
gridcoinresearchd_LDFLAGS = $(RELDFLAGS) $(AM_LDFLAGS) $(LIBTOOL_APP_LDFLAGS)

gridcoinresearchd_LDADD = \
 $(LIBGRIDCOIN_UTIL) \
 $(LIBGRIDCOIN_CRYPTO) \
 $(LIBUNIVALUE) \
 $(LIBLEVELDB) \
 $(LIBLEVELDB_SSE42) \
 $(LIBMEMENV)

gridcoinresearchd_LDADD += $(BOOST_LIBS) $(BDB_LIBS) $(SSL_LIBS) $(CRYPTO_LIBS) $(MINIUPNPC_LIBS) $(EVENT_PTHREADS_LIBS) $(EVENT_LIBS)

if TARGET_WINDOWS
gridcoinresearchd_SOURCES += gridcoinresearchd-res.rc
gridcoinresearchd_CPPFLAGS += -DUNICODE
endif

CLEANFILES = $(EXTRA_LIBRARIES)
CLEANFILES += univalue/*.gcda univalue/*.gcno
CLEANFILES += *.gcda *.gcno
CLEANFILES += compat/*.gcda compat/*.gcno
CLEANFILES += crypto/*.gcda crypto/*.gcno
CLEANFILES += obj/build.h

EXTRA_DIST = $(CTAES_DIST)


config/gridcoin-config.h: config/stamp-h1
	@$(MAKE) -C $(top_builddir) $(subdir)/$(@)
config/stamp-h1: $(top_srcdir)/$(subdir)/config/gridcoin-config.h.in $(top_builddir)/config.status
	$(AM_V_at)$(MAKE) -C $(top_builddir) $(subdir)/$(@)
$(top_srcdir)/$(subdir)/config/gridcoin-config.h.in:  $(am__configure_deps)
	$(AM_V_at)$(MAKE) -C $(top_srcdir) $(subdir)/config/gridcoin-config.h.in

clean-local:
	-$(MAKE) -C univalue clean
	-rm -f leveldb/*/*.gcda leveldb/*/*.gcno leveldb/helpers/memenv/*.gcda leveldb/helpers/memenv/*.gcno
	-rm -f config.h
	-rm -rf test/__pycache__

.rc.o:
	@test -f $(WINDRES)
	## FIXME: How to get the appropriate modulename_CPPFLAGS in here?
	$(AM_V_GEN) $(WINDRES) $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(CPPFLAGS) -DWINDRES_PREPROC -i $< -o $@

%.pb.cc %.pb.h: %.proto
	@test -f $(PROTOC)
	$(AM_V_GEN) $(PROTOC) --cpp_out=$(@D) --proto_path=$(<D) $<

if EMBEDDED_LEVELDB
include Makefile.leveldb.include
endif

if ENABLE_QT
include Makefile.qt.include
endif

if ENABLE_TESTS
include Makefile.test.include
endif

if ENABLE_QT_TESTS
include Makefile.qttest.include
endif
