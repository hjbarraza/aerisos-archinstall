# AerisOS archinstall config

An [archinstall](https://github.com/archlinux/archinstall) configuration with every AerisOS repo package preselected. It is the first step of a new AerisOS machine; the second is `install.sh` from [aerisos](https://github.com/hjbarraza/aerisos).

## Install

Boot the stock Arch ISO, connect to the network (`iwctl` for Wi-Fi), then:

```bash
archinstall --config-url https://raw.githubusercontent.com/hjbarraza/aerisos-archinstall/main/user_configuration.json
```

The menu opens with the AerisOS packages, PipeWire, NetworkManager, systemd-boot, multilib, zram swap and the hostname `aeris` already set. Pick the **disk**, **user**, **timezone** and **graphics driver**, then Install.

The install clones aerisos to `/root/aerisos`. After the reboot, log in as root and run:

```bash
bash /root/aerisos/install.sh
```

That adds the AUR packages, the AerisOS configs and, on NVIDIA machines, the NVIDIA drivers, CUDA and Steam (left out here so other GPUs don't get them).

Offline: copy `user_configuration.json` to a USB stick and use `archinstall --config /path/to/user_configuration.json`.

Not for T2 Macs: they need the AerisOS installer USB (`iso/build.sh --t2` in aerisos).

## Updating

`user_configuration.json` is generated from `packages/pacman.txt` in aerisos. `./setup.sh snapshot` there runs `make-config` when this repo is checked out next to it (`~/aerisos-archinstall`); commit and push the result here. By hand: `./make-config [~/aerisos]`.

Checked against archinstall 4.5.
