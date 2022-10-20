# distccd-alarm

Toolchain and systemd services to use x86_64 volunteers to help build Arch ARM stuff.

## Real speed gains compiling on Arch ARM can be realized with a single x86_64 volunteer.
The following examples illustrate that gains for 2-3x can be realized when compiling ARM code using a single x86_64 volunteer with distcc. The two compile tasks shown below used a RPi4 host alone, then the RPi4 host with a single x86_64.

For the purposes of the experiments, two different x86_64 volunteers were used:
* Hostname mars was an Intel i7-4790k (quad core) running Arch Linux (x86_64).
* Hostname mercury was an Intel i3-4130T (dual core) running Arch Linux (x86_64).
* Compilation on the RPi4 alone was `make -j5 bzImage` for the kernel and `make -j5` for ffmpeg.
* Compilation on the RPi4 using distcc was `make -j5 bzImage CC=distcc CXX=distcc` for the kernel and `make -j16` for ffmpeg.

### Linux kernel

Building kernel v5.4.75 (`make bzImage` only). The table below summarizes the runs compiling alone and with the x86_64 node.  The times shown are the mean of 4 runs.  The % change is relative to the time to compile alone.  Using a single x86_64 node decreases compilation time by 2.1-2.6x depending on the CPU power of the volunteer tested.

| Nodes   | Time (sec)  | % change|
| -------- | :-----:| :----:|
| RPi4 alone   |  1,341.3 ± 1.1 | -
| RPi4+mars | 516.2 ± 0.4 | 260.0
| RPi4+mercury | 639.0 ± 0.9  | 210.0

### Ffmpeg

Building ffmpeg v4.3.1, the table below summarizes the runs compiling alone and with the x86_64 node.  The times shown are the mean of 4 runs.  The % change is relative to the time to compile alone.  Using a single x86_64 node decreases compilation time by by 2.1-3.3x depending on the CPU power of the volunteer tested.

| Nodes   | Time (sec)  | % change|
| -------- | :-----:| :----:|
| RPi4 alone   |  757.1 ± 0.7 | -
| RPi4+mars | 229.4 ± 5.0  | 330.0
| RPi4+mercury | 356.6 ± 0.1 | 212.3

## Download a pre-built package
Arch ARM supplies pre-built toolchains for armv7h and armv8 (aarch64) and the [distccd-alarm](https://aur.archlinux.org/packages/distccd-alarm-armv7h/) package in the [AUR](https://aur.archlinux.org/) supplies these plus systemd service units.  Download and install these on your x86_64 volunteer.

## Links
* https://archlinuxarm.org/wiki/Distcc_Cross-Compiling
* https://wiki.archlinux.org/index.php/Distcc#Arch_Linux_ARM_as_clients_(x86_64_as_volunteers)
