# combo driver: MT6620
# If KERNELRELEASE is defined, we've been invoked from the
# kernel build system and can use its language.
ifneq ($(KERNELRELEASE),)
	
	COMBO_CHIP_SUPPORT := false
	ifneq ($(filter MT6620E3,$(MTK_COMBO_CHIP)),)
		COMBO_CHIP_SUPPORT := true
	endif

	ifneq ($(filter MT6628,$(MTK_COMBO_CHIP)),)
		COMBO_CHIP_SUPPORT := true
	endif
	
	ifneq ($(filter MT6630,$(MTK_COMBO_CHIP)),)
		COMBO_CHIP_SUPPORT := true
	endif
	
	ifeq ($(COMBO_CHIP_SUPPORT), true)
		subdir-ccflags-y += -D MTK_WCN_COMBO_CHIP_SUPPORT
		COMBO_FOLDER := ../combo/common
		ccflags-y += -I$(src)/$(COMBO_FOLDER)/linux/include
	endif
	
	SOC_CHIP_SUPPORT := false
	ifneq ($(filter CONSYS_6592,$(MTK_COMBO_CHIP)),)
		SOC_CHIP_SUPPORT := true
	endif
	ifneq ($(filter CONSYS_6582,$(MTK_COMBO_CHIP)),)
		SOC_CHIP_SUPPORT := true
	endif
	ifneq ($(filter CONSYS_6572,$(MTK_COMBO_CHIP)),)
		SOC_CHIP_SUPPORT := true
	endif
	ifneq ($(filter CONSYS_6571,$(MTK_COMBO_CHIP)),)
		SOC_CHIP_SUPPORT := true
	endif
	
	ifeq ($(SOC_CHIP_SUPPORT), true)
		subdir-ccflags-y += -D MTK_WCN_SOC_CHIP_SUPPORT
		CONN_COMMON := ../combo/common
		ccflags-y += -I$(src)/$(CONN_COMMON)/linux/include
	endif
	
	
ifeq ($(CONFIG_MTK_COMBO),y)
	ccflags-y += -I$(src)/drv_init/inc 	
	obj-y += mtk_wcn_stub_alps.o
	obj-y += wmt_stp_exp.o
	
	obj-y += wmt_detect.o
	obj-y += sdio_detect.o
	obj-y += wmt_detect_pwr.o
	
	obj-y += drv_init/
	
endif
	
ifeq ($(CONFIG_MTK_COMBO),m)
	obj-y += mtk_wcn_stub_alps.o
	obj-y += wmt_stp_exp.o
	
	obj-$(CONFIG_MTK_COMBO) += mtk_wmt_detect.o
	mtk_wmt_detect-objs := wmt_detect.o
	mtk_wmt_detect-objs += sdio_detect.o
	mtk_wmt_detect-objs += wmt_detect_pwr.o

endif
  
# Otherwise we were called directly from the command
# line; invoke the kernel build system.
else
    KERNELDIR ?= /lib/modules/$(shell uname -r)/build
    PWD  := $(shell pwd)
default:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules
endif
