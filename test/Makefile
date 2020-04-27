DTC=/opt/intelFPGA/16.1/embedded/host_tools/gnu/dtc/dtc

PRELOADER_DIR=.
PRELOADER=$(PRELOADER_DIR)/preloader-mkpimage.bin

SDCARD=/dev/mmcblk0
SDCARDMP1=/media/mmcblk0p1

DATETIME=$(shell date --iso=seconds)

all: m1_dma

%.dtb: %.dts 
	$(DTC) -I dts -O dtb -o $@ $<

%.rbf: %.sof
	quartus_cpf -c $< $@

sdcard: ../fpga/fpga.rbf soc_m1_minimal.dtb $(PRELOADER) /dev/mmcblk0p1 /dev/mmcblk0p3
	pmount $(SDCARD)p1 $(SDCARDMP1); true
	cp ../fpga/fpga.rbf $(SDCARDMP1)/soc_system.rbf
	cp soc_m1_minimal.dtb $(SDCARDMP1)/socfpga.dtb
	sudo dd if=$(PRELOADER) of=$(SDCARD)p3 bs=64k seek=0
	pumount $(SDCARD)p1
	sync
