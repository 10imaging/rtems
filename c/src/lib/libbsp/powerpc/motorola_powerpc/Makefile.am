ACLOCAL_AMFLAGS = -I ../../../../aclocal
EXTRA_DIST =

_SUBDIRS  = .
_SUBDIRS += bootloader
if QEMU
_SUBDIRS += qemu_fakerom
endif

include $(top_srcdir)/../../../../automake/compile.am
include $(top_srcdir)/../../bsp.am

include_bspdir = $(includedir)/bsp

dist_project_lib_DATA = bsp_specs

include_HEADERS = include/bsp.h
include_HEADERS += include/tm27.h

nodist_include_HEADERS = include/bspopts.h
nodist_include_bsp_HEADERS = ../../shared/include/bootcard.h
DISTCLEANFILES = include/bspopts.h

noinst_PROGRAMS =

include_HEADERS += ../../powerpc/shared/include/nvram.h

EXTRA_DIST += ../../powerpc/shared/start/start.S
start.$(OBJEXT): ../../powerpc/shared/start/start.S
	$(CPPASCOMPILE) -o $@ -c $<
project_lib_DATA = start.$(OBJEXT)

EXTRA_DIST += ../../powerpc/shared/start/rtems_crti.S
rtems_crti.$(OBJEXT): ../../powerpc/shared/start/rtems_crti.S
	$(CPPASCOMPILE) -o $@ -c $<
project_lib_DATA += rtems_crti.$(OBJEXT)

EXTRA_DIST += ../../powerpc/shared/start/vectors_entry.S
vectors_entry.$(OBJEXT): ../../powerpc/shared/start/vectors_entry.S
	$(CPPASCOMPILE) -o $@ -c $<
project_lib_DATA += vectors_entry.$(OBJEXT)

dist_project_lib_DATA += ../shared/startup/linkcmds.share
dist_project_lib_DATA += startup/linkcmds

noinst_LIBRARIES = libbsp.a
libbsp_a_SOURCES =

# startup
libbsp_a_SOURCES += ../../powerpc/shared/startup/bspstart.c \
 	../../powerpc/shared/startup/bspgetworkarea.c \
 	../../powerpc/shared/showbats.c \
    ../../powerpc/shared/startup/bsppredriverhook.c \
 	../../powerpc/shared/startup/zerobss.c \
    ../../powerpc/shared/startup/pgtbl_setup.c \
    ../../powerpc/shared/startup/pgtbl_activate.c \
	../../powerpc/shared/startup/ppc_idle.c \
    ../../powerpc/shared/startup/sbrk.c ../../shared/bootcard.c \
    ../../shared/getentropy-cpucounter.c \
    ../../shared/bspclean.c \
    ../../shared/gnatinstallhandler.c \
    startup/bspreset.c


# tod
libbsp_a_SOURCES += ../../shared/tod.c ../../powerpc/shared/tod/todcfg.c
# pclock
libbsp_a_SOURCES += ../../powerpc/shared/clock/p_clock.c

include_bsp_HEADERS = ../../powerpc/shared/console/consoleIo.h
include_bsp_HEADERS += ../../powerpc/shared/console/uart.h

# Needs conditional compilation
polledIO_CPPFLAGS = -DSTATIC_LOG_ALLOC
noinst_PROGRAMS += polledIO.rel
polledIO_rel_SOURCES = ../../powerpc/shared/console/polled_io.c
polledIO_rel_CPPFLAGS = $(AM_CPPFLAGS) $(polledIO_CPPFLAGS)
polledIO_rel_LDFLAGS = $(RTEMS_RELLDFLAGS)

# console
libbsp_a_SOURCES += ../../powerpc/shared/console/uart.c
libbsp_a_SOURCES += ../../powerpc/shared/console/console.c
libbsp_a_SOURCES += ../../powerpc/shared/console/consoleIo.h
libbsp_a_SOURCES += ../../powerpc/shared/console/keyboard.h
libbsp_a_SOURCES += ../../powerpc/shared/console/uart.h

include_bsp_HEADERS += include/bsp/irq.h

# irq
libbsp_a_SOURCES += ../../powerpc/shared/irq/irq_init.c
libbsp_a_SOURCES += ../../powerpc/shared/irq/openpic_i8259_irq.c
libbsp_a_SOURCES += ../../powerpc/shared/irq/i8259.c

include_bsp_HEADERS += ../../powerpc/shared/motorola/motorola.h
# motorola
libbsp_a_SOURCES += ../../powerpc/shared/motorola/motorola.h
libbsp_a_SOURCES += ../../powerpc/shared/motorola/motorola.c

include_bsp_HEADERS += ../../powerpc/shared/openpic/openpic.h
# openpic
libbsp_a_SOURCES += ../../powerpc/shared/openpic/openpic.h
libbsp_a_SOURCES += ../../powerpc/shared/openpic/openpic.c
libbsp_a_SOURCES += ../../powerpc/shared/openpic/openpic.h

include_bsp_HEADERS += ../../powerpc/shared/pci/pci.h
# pci
libbsp_a_SOURCES += ../../powerpc/shared/pci/pci.c
libbsp_a_SOURCES += ../../powerpc/shared/pci/detect_raven_bridge.c
libbsp_a_SOURCES += ../../powerpc/shared/pci/generic_clear_hberrs.c
libbsp_a_SOURCES += ../../powerpc/shared/pci/pcifinddevice.c
libbsp_a_SOURCES += ../../powerpc/shared/pci/pci.h

include_bsp_HEADERS += ../../powerpc/shared/residual/residual.h \
    ../../powerpc/shared/residual/pnp.h
# residual
libbsp_a_SOURCES += ../../powerpc/shared/residual/pnp.h
libbsp_a_SOURCES += ../../powerpc/shared/residual/residual.h
libbsp_a_SOURCES += ../../powerpc/shared/residual/residual.c

include_bsp_HEADERS += ../../shared/vmeUniverse/vmeUniverse.h \
    ../../shared/vmeUniverse/vme_am_defs.h \
    ../../shared/vmeUniverse/VME.h \
    include/bsp/VMEConfig.h \
    ../../shared/vmeUniverse/vmeUniverseDMA.h\
    ../../shared/vmeUniverse/bspVmeDmaList.h\
    ../../shared/vmeUniverse/VMEDMA.h
# vme
libbsp_a_SOURCES += ../../shared/vmeUniverse/vmeUniverse.c
libbsp_a_SOURCES += ../../shared/vmeUniverse/bspVmeDmaList.c
libbsp_a_SOURCES += ../../shared/vmeUniverse/vmeUniverse.h
libbsp_a_SOURCES += ../../shared/vmeUniverse/vme_am_defs.h
libbsp_a_SOURCES += ../../shared/vmeUniverse/VME.h
libbsp_a_SOURCES += ../../powerpc/shared/vme/vmeconfig.c
libbsp_a_SOURCES += ../../powerpc/shared/vme/vme_universe.c

if QEMU
if HAS_NETWORKING
ne2000_CPPFLAGS          = -D__INSIDE_RTEMS_BSD_TCPIP_STACK__
ne2000_CPPFLAGS         += '-Dbsp_cmdline_arg=rtems_bsp_cmdline_get_param_raw'
noinst_PROGRAMS         += ne2000.rel
ne2000_rel_SOURCES       = ../../i386/pc386/ne2000/ne2000.c
ne2000_rel_CPPFLAGS      = $(AM_CPPFLAGS) $(ne2000_CPPFLAGS)
ne2000_rel_LDFLAGS       = $(RTEMS_RELLDFLAGS)
endif
endif

libbsp_a_LIBADD = \
    polledIO.rel \
    ../../../libcpu/@RTEMS_CPU@/shared/cache.rel \
    ../../../libcpu/@RTEMS_CPU@/shared/cpuIdent.rel \
    ../../../libcpu/@RTEMS_CPU@/shared/stack.rel \
    ../../../libcpu/@RTEMS_CPU@/@exceptions@/rtems-cpu.rel \
    ../../../libcpu/@RTEMS_CPU@/mpc6xx/clock.rel \
    ../../../libcpu/@RTEMS_CPU@/@exceptions@/exc_bspsupport.rel \
    ../../../libcpu/@RTEMS_CPU@/@exceptions@/irq_bspsupport.rel \
    ../../../libcpu/@RTEMS_CPU@/mpc6xx/mmu.rel \
    ../../../libcpu/@RTEMS_CPU@/mpc6xx/timer.rel \
    ../../../libcpu/@RTEMS_CPU@/mpc6xx/altivec.rel

if QEMU
if HAS_NETWORKING
libbsp_a_LIBADD+=ne2000.rel
endif
endif

EXTRA_DIST += BOOTING README.mtx603e README.MVME2100 README.MVME2300 \
              README.MVME2400 \
    README.OTHERBOARDS
EXTRA_DIST += README.dec21140
EXTRA_DIST += times.mcp750 times.mvme2307

include $(srcdir)/preinstall.am
include $(top_srcdir)/../../../../automake/local.am
include $(top_srcdir)/../../../../automake/subdirs.am
