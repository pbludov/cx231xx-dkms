INSTALL := $(shell which install)

cx231xx-objs      := cx231xx-video.o cx231xx-i2c.o cx231xx-cards.o cx231xx-core.o \
                     cx231xx-avcore.o cx231xx-417.o cx231xx-pcb-cfg.o cx231xx-vbi.o cx231xx-input.o

cx231xx-alsa-objs := cx231xx-audio.o
cx231xx-dvb-objs  := cx231xx-dvb.o

obj-m      += cx231xx.o
obj-alsa-m += cx231xx-alsa.o
obj-dvb-m  += cx231xx-dvb.o

EXTRA_CFLAGS += -Idrivers/media/i2c
EXTRA_CFLAGS += -Idrivers/media/tuners
EXTRA_CFLAGS += -Idrivers/media/dvb-core
EXTRA_CFLAGS += -Idrivers/media/dvb-frontends
EXTRA_CFLAGS += -Idrivers/media/usb/dvb-usb

default: 
	make -C $(KERNELDIR) O=$(KERNELDIR) SUBDIRS=`pwd` modules

install:
	rm -f /lib/modules/$(KERNELRELEASE)/kernel/drivers/media/usb/cx231xx/*.ko
	$(INSTALL) -c -D -m 644 -c cx231xx.ko /lib/modules/$(KERNELRELEASE)/kernel/drivers/media/usb/cx231xx/
	$(INSTALL) -c -D -m 644 -c cx231xx-alsa.ko /lib/modules/$(KERNELRELEASE)/kernel/drivers/media/usb/cx231xx/
	$(INSTALL) -c -D -m 644 -c cx231xx-dvb.ko /lib/modules/$(KERNELRELEASE)/kernel/drivers/media/usb/cx231xx/
	/sbin/depmod -a

clean:
	-rm -fr *~ *.o *.ko .*.o.cmd .*.ko.cmd .*.o.d *.mod.c *.*~ Module.symvers modules.order .tmp_versions

-include $(KERNELDIR)/Rules.make
