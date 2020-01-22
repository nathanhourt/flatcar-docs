# Migrating from CoreOS Container Linux

While Flatcar is compatible with CoreOS Container Linux there are some naming differences you need to be aware of.

**NOTE:** See [Updating from CoreOS Container Linux](https://docs.flatcar-linux.org/os/update-from-container-linux/)
for additional information on updating an existing cluster.

## Installation

Instead of `coreos-installer` you need to use `flatcar-installer`.

## Kernel command line parameters

Instead of providing the `coreos.first_boot=1` argument via the boot loader you need to provide `flatcar.first_boot=1`.
This forces provisioning via Ignition even if the machine (image) was booted already before.

Instead of providing the `coreos.config.url=SOMEURL` argument via the boot loader you need to provide `ignition.config.url=SOMEURL`
to tell Ignition to download the configuration.
The change to a more generic name was done upstream by the Ignition project. Version 0.33 still supports both names and we
also do this via the analogous `flatcar.config.url` option but we encourage the generic name because future versions of Ignition
will only support `ignition.config.url`.

## Ignition configuration with QEMU

Instead of using `opt/com.coreos/config` in the `-fw_cfg` name-value argument pair for QEMU/KVM or libvirt you need to use `opt/org.flatcar-linux/config`.
The value in the argument pair specifies the Ignition file to use.

## Ignition configuration with VMware

Instead of `coreos.config.data` and `coreos.config.data.encoding` for the VMware `guestinfo.VARIABLE` command line options you need
to use `ignition.config.data` and `ignition.config.data.encoding`.
As for the kernel parameter this change was done upstream by the Ignition project.