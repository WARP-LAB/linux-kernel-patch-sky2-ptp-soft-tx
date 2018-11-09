# Software PTP TX Linux kernel driver patch for Marvell ethernet

## How

* Copy patch in Linux kernel source directory
* `cd` into source directory
* Apply the patch

	```sh
	patch -p1 < sky2.patch
	```
* Rebuild kernel as usual

## Why

To be able to test PTP software & slave-only mode on some old HW which uses *Marvell Yukon Gigabit Ethernet Controller*.

Before

```
ethtool -T ens5
Time stamping parameters for ens5:
Capabilities:
    software-receive      (SOF_TIMESTAMPING_RX_SOFTWARE)
    software-system-clock (SOF_TIMESTAMPING_SOFTWARE)
PTP Hardware Clock: none
Hardware Transmit Timestamp Modes: none
Hardware Receive Filter Modes: none
```

After

```
ethtool -T ens5
Time stamping parameters for ens5:
Capabilities:
    software-transmit     (SOF_TIMESTAMPING_TX_SOFTWARE)
    software-receive      (SOF_TIMESTAMPING_RX_SOFTWARE)
    software-system-clock (SOF_TIMESTAMPING_SOFTWARE)
PTP Hardware Clock: none
Hardware Transmit Timestamp Modes: none
Hardware Receive Filter Modes: none
```

And `ptp4l` at least launches

