# SPDX-License-Identifier: GPL-2.0

ccflags-$(CONFIG_USB_MTU3_DEBUG)	+= -DDEBUG

ifneq ($(CONFIG_USB_MTU3_PLAT_PHONE),)
ccflags-y += -I$(srctree)/drivers/misc/mediatek/include/
ccflags-y += -I$(srctree)/drivers/power/supply/mediatek/misc/
ifeq ($(CONFIG_AGATE_CHARGER),y)
ccflags-y += -I$(srctree)/drivers/misc/mediatek/typec/tcpc_agate/
else ifeq ($(CONFIG_ARES_CHARGER),y)
ccflags-y += -I$(srctree)/drivers/misc/mediatek/typec/tcpc_ares/
else ifeq ($(CONFIG_PISSARRO_CHARGER),y)
ccflags-y += -I$(srctree)/drivers/misc/mediatek/typec/tcpc_pissarro
else
ccflags-y += -I$(srctree)/drivers/misc/mediatek/typec/tcpc/
endif
ifeq ($(CONFIG_MACH_MT6877),y)
ccflags-y += -I$(srctree)/drivers/usb/mtu3/mt6877/
else
ccflags-y += -I$(srctree)/drivers/usb/mtu3/$(CONFIG_MTK_PLATFORM)/
endif
endif

ifneq ($(CONFIG_USB_MTU3_PLAT_PHONE),)

ifeq ($(CONFIG_MACH_MT6877),y)
obj-y += $(subst ",,mt6877)/
else
obj-y += $(subst ",,$(CONFIG_MTK_PLATFORM))/
endif
obj-y += mtu3_debugfs_v2.o

obj-$(CONFIG_USB_MTU3)	+= musb_hdrc.o

musb_hdrc-y	:= mtu3_plat_v2.o

ifneq ($(filter y,$(CONFIG_USB_MTU3_HOST) $(CONFIG_USB_MTU3_DUAL_ROLE)),)
	musb_hdrc-y	+= mtu3_host_v2.o
endif

ifneq ($(filter y,$(CONFIG_USB_MTU3_GADGET) $(CONFIG_USB_MTU3_DUAL_ROLE)),)
	musb_hdrc-y	+= mtu3_core.o mtu3_gadget_ep0.o mtu3_gadget.o mtu3_qmu.o
endif

ifneq ($(CONFIG_USB_MTU3_DUAL_ROLE),)
	musb_hdrc-y	+= mtu3_dr_v2.o
endif

else

subdir-ccflags-y += -I$(srctree)/drivers/misc/mediatek/include/mt-plat

ifneq ($(filter y,$(CONFIG_MACH_MT8168)),)
subdir-ccflags-y += -I$(srctree)/drivers/misc/mediatek/base/power/mt8168/
endif


obj-$(CONFIG_USB_MTU3) += mtu3.o

mtu3-y := mtu3_plat.o

ifneq ($(filter y,$(CONFIG_USB_MTU3_HOST) $(CONFIG_USB_MTU3_DUAL_ROLE)),)
	mtu3-y	+= mtu3_host.o
endif

ifneq ($(filter y,$(CONFIG_USB_MTU3_GADGET) $(CONFIG_USB_MTU3_DUAL_ROLE)),)
	mtu3-y	+= mtu3_core.o mtu3_gadget_ep0.o mtu3_gadget.o mtu3_qmu.o
endif

ifneq ($(CONFIG_USB_MTU3_DUAL_ROLE),)
ifeq ($(CONFIG_AGATE_CHARGER),y)
	mtu3-y	+= mtu3_dr_agate.o
else
	mtu3-y	+= mtu3_dr.o
endif
endif

endif
