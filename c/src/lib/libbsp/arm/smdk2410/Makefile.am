ACLOCAL_AMFLAGS = -I ../../../../aclocal
EXTRA_DIST =

include $(top_srcdir)/../../../../automake/compile.am
include $(top_srcdir)/../../bsp.am

include_bspdir = $(includedir)/bsp

dist_project_lib_DATA = bsp_specs

include_HEADERS = include/bsp.h
include_HEADERS += smc/smc.h
include_HEADERS += include/tm27.h
include_HEADERS += include/s3c24xx.h
include_HEADERS += include/s3c2400.h
include_HEADERS += include/s3c2410.h

include_bsp_HEADERS =
libbsp_a_CPPFLAGS =

nodist_include_HEADERS = include/bspopts.h
nodist_include_bsp_HEADERS = ../../shared/include/bootcard.h
DISTCLEANFILES = include/bspopts.h

EXTRA_DIST += start/start.S
start.$(OBJEXT): start/start.S
	$(CPPASCOMPILE) -o $@ -c $<
project_lib_DATA = start.$(OBJEXT)

dist_project_lib_DATA += startup/linkcmds

noinst_LIBRARIES = libbsp.a
libbsp_a_SOURCES =

# startup
libbsp_a_SOURCES += startup/bspstart.c
libbsp_a_SOURCES += startup/bspidle.c
libbsp_a_SOURCES += ../../shared/bspclean.c
libbsp_a_SOURCES += startup/bspreset.c
libbsp_a_SOURCES += startup/memmap.c
libbsp_a_SOURCES += ../../shared/bootcard.c
libbsp_a_SOURCES += ../../shared/getentropy-cpucounter.c
libbsp_a_SOURCES += ../../shared/sbrk.c

libbsp_a_SOURCES += ../../shared/bsppredriverhook.c
libbsp_a_SOURCES += ../../shared/bspgetworkarea.c
libbsp_a_SOURCES += ../../shared/gnatinstallhandler.c
libbsp_a_SOURCES += ../../shared/cpucounterread.c
libbsp_a_SOURCES += ../../shared/cpucounterdiff.c
libbsp_a_SOURCES += timer/timer.c
libbsp_a_SOURCES += clock/clockdrv.c
libbsp_a_SOURCES += clock/support.c
# console
libbsp_a_SOURCES += console/uart.c
libbsp_a_SOURCES += ../../shared/console.c
libbsp_a_SOURCES += ../../shared/console_select.c
libbsp_a_SOURCES += ../../shared/console_read.c
libbsp_a_SOURCES += ../../shared/console_write.c
libbsp_a_SOURCES += ../../shared/console_control.c
# IRQ
include_bsp_HEADERS += ../../shared/include/irq-generic.h \
	../../shared/include/irq-info.h
include_bsp_HEADERS += include/bsp/irq.h
libbsp_a_SOURCES += ../../shared/src/irq-default-handler.c
libbsp_a_SOURCES += ../../shared/src/irq-generic.c
libbsp_a_SOURCES += ../../shared/src/irq-info.c
libbsp_a_SOURCES += ../../shared/src/irq-legacy.c
libbsp_a_SOURCES += ../../shared/src/irq-server.c
libbsp_a_SOURCES += ../../shared/src/irq-shell.c
libbsp_a_SOURCES += irq/irq.c
# smc
libbsp_a_SOURCES += smc/smc.c
libbsp_a_SOURCES += smc/smc.h

# Cache
libbsp_a_SOURCES += ../../../libcpu/shared/src/cache_manager.c
libbsp_a_SOURCES += ../shared/include/arm-cache-l1.h
libbsp_a_SOURCES += ../shared/armv467ar-basic-cache/cache_.h
libbsp_a_CPPFLAGS += -I$(srcdir)/../shared/armv467ar-basic-cache

libbsp_a_LIBADD = ../../../libcpu/@RTEMS_CPU@/shared/arm920.rel

include $(srcdir)/preinstall.am
include $(top_srcdir)/../../../../automake/local.am
