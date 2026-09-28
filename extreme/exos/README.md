# vrnetlab / Extreme-EXOS (exos)

This is the vrnetlab docker image for Extreme EXOS.

## Building the docker image

Select and download the QCOW2 image from [Extreme Networks github page](https://github.com/extremenetworks/Virtual_EXOS?tab=readme-ov-file#qcow2-files-for-gns3), or if you know the version you want you can directly use this:

```bash
curl -O https://akamai-ep.extremenetworks.com/Extreme_P/github-en/Virtual_EXOS/EXOS-VM_32.7.2.19.qcow2
```

Place the QCOW2 image into this folder, then run:

```bash
make
```

The image will be tagged based on the version in the filename (e.g., `vrnetlab/extreme_exos:32.7.2.19`).

## Running on an AMD CPU

EXOS does not boot on a host with an AMD CPU with the default `-cpu host`. The console shows `Warning. Could not determine the CPU Family.` and the VM stops at the EXOS developer menu, so the bootstrap never completes.

Workaround: set the `QEMU_CPU` environment variable to `core2duo`, e.g. in a containerlab topology:

```yaml
    env:
      QEMU_CPU: core2duo
```

This was tested with 32.6.3.126 and 32.7.2.19 on an AMD EPYC host.

It does not work for 33.1.1.31 on an AMD CPU.

## Tested versions

| Image                       | Intel CPU | AMD CPU                                 |
| --------------------------- | --------- | --------------------------------------- |
| `EXOS-VM_v32.6.3.126.qcow2` | OK.       | OK with `QEMU_CPU=core2duo`             |
| `EXOS-VM_32.7.2.19.qcow2`   | OK        | OK with `QEMU_CPU=core2duo`             |
| `EXOS-VM_33.1.1.31.qcow2`   | OK        | NOK, no working settings found          |
