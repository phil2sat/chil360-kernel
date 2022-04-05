#ar6000
obj-m += ar6000.o

ar6000-y += debug.o debugfs_pri.o hif.o htc.o bmi.o cfg80211.o
ar6000-y += cfg80211_btcoex.o pm.o init.o main.o txrx.o wmi.o wmi_btcoex.o
ar6000-y += sdio.o platform.o softmac.o wmiconfig.o regd.o testmode.o
ar6000-y += recovery.o

ccflags-y += -D__CHECK_ENDIAN__
ccflags-y += -DCONFIG_ATH6KL_DEBUG
ccflags-y += -DCONFIG_CFG80211
ccflags-y += -DCONFIG_CFG80211_DEFAULT_PS
ccflags-y += -DCONFIG_CFG80211_WEXT
ccflags-y += -DCONFIG_NL80211_TESTMODE

ccflags-y += -DFIX_HUAWEI_BUTCHERING

SELF_DIR := $(dir $(lastword $(MAKEFILE_LIST)))

ccflags-y += -I$(SELF_DIR)/../include
ccflags-y += -I$(SELF_DIR)/../ar6000
ccflags-y += -include $(SELF_DIR)/../include/linux/ieee80211.h
ccflags-y += -include $(SELF_DIR)/../include/linux/nl80211.h
ccflags-y += -include $(SELF_DIR)/../include/net/cfg80211.h
ccflags-y += -include $(SELF_DIR)/../include/linux/compat-2.6.h

ldflags-y += --strip-debug

KBUILD_EXTRA_SYMBOLS = $(SELF_DIR)/../cfg80211/Module.symvers

KERNELDIR ?=KERNELDIR=/lib/modules/${_abi_release}/build

modules:
	$(MAKE) -C $(KERNELDIR) M=`pwd` ARCH=arm CROSS_COMPILE=$(CROSS_COMPILE) modules

clean:
	$(MAKE) -C $(KERNELDIR) M=`pwd` ARCH=arm CROSS_COMPILE=$(CROSS_COMPILE) clean
