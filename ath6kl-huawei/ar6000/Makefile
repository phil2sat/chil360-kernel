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

ifeq ($(strip $(WIFI_FIX_HUAWEI_BUTCHERING)),true)
ccflags-y += -DFIX_HUAWEI_BUTCHERING
endif

ifeq ($(strip $(AR6005_SELF_INIT_SUPPORT)),true)
ccflags-y += -DAR6005_SELF_INIT_SUPPORT
endif

ifeq ($(strip $(WIFI_POWER_TUNED)),true)
ccflags-y += -DWIFI_POWER_TUNED
endif

ifeq ($(strip $(WIFI_MAC_FROM_NV)),true)
ccflags-y += -DWIFI_MAC_FROM_NV
endif

ccflags-y += -DWIFI_DRIVER_IFACE_NAME=\"$(WIFI_DRIVER_IFACE_NAME)\"
ccflags-y += -DWIFI_DRIVER_MODULE_PATH=\"$(WIFI_DRIVER_MODULE_PATH)\"
ccflags-y += -DWIFI_DRIVER_MODULE_NAME=\"$(WIFI_DRIVER_MODULE_NAME)\"

ccflags-y += -DAR6003_MAC_FILE=\"$(AR6003_MAC_FILE)\"
ccflags-y += -DAR6003_REV2_BOARD_POWER_PA_FILE=\"$(AR6003_REV2_BOARD_POWER_PA_FILE)\"
ccflags-y += -DAR6003_HW_FW_DIR=\"$(AR6003_HW_FW_DIR)\"
ccflags-y += -DAR6003_HW_BOARD_DATA_FILE=\"$(AR6003_HW_BOARD_DATA_FILE)\"
ccflags-y += -DAR6003_HW_DEFAULT_BOARD_DATA_FILE=\"$(AR6003_HW_DEFAULT_BOARD_DATA_FILE)\"

ATH_ROOT = $(src)/..

ccflags-y += -I$(ATH_ROOT)/include
ccflags-y += -I$(ATH_ROOT)/ar6000
ccflags-y += -include $(ATH_ROOT)/include/linux/ieee80211.h
ccflags-y += -include $(ATH_ROOT)/include/linux/nl80211.h
ccflags-y += -include $(ATH_ROOT)/include/net/cfg80211.h
ccflags-y += -include $(ATH_ROOT)/include/linux/compat-2.6.h

ldflags-y += --strip-debug

KBUILD_EXTRA_SYMBOLS = $(ATH_ROOT)/cfg80211/Module.symvers

modules:
	$(MAKE) -C $(KERNEL_OUT) M=`pwd` ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) modules

clean:
	$(MAKE) -C $(KERNEL_OUT) M=`pwd` ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) clean
