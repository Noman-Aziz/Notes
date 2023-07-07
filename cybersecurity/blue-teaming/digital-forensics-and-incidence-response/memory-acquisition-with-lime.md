# Memory Acquisition with LIME

### Memory Acquisition

Aka Memory Dump is process of dumping RAM from specific systems to disk for purpose of analysis



### LIME

* It is a Loadable Kernel Module (LKM) used for acquisition of volatile memory from **Linux** and linux based devices like **Android**
* It supports exporting memory dump either to file system of device or over the network
* Since it is a LKM, it needs to be compiled on the system which has same kernel version with of the infected system on which you want to dump memory and then it can be transfered to the infected machine



### Prerequisites to install

1. gcc
2. cmake
3. build-essential



### Steps to install

Goto `src` directory and `make`



### Steps to Run

`insmod ./lime-<kernel-version>.ko "path=/root/dump.mem format=raw"`

* Path is where to store the dump
* format raw means that this will be compatible with other forensic tools with Memory Forensice with Volatility
* **Size of the dump will be will same as RAM i.e 8GB Ram = 8GB Dump**

