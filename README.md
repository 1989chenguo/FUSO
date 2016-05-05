# What is FUSO?
FUSO is a fast multi-path transport loss recovery scheme for data centers, which attempts to be both "fast" and "cautious".
Currently, FUSO is a kernel transport implementation which is built upon [MPTCP’s Linux implementation (v0.90)](http://multipath-tcp.org/pmwiki.php?n=Main.Release90).

For more details about FUSO, please refer to our USENIX ATC 2016 paper "Fast and Cautious: Leveraging Multi-path Diversity for Transport Loss Recovery in Data Centers"

# How to use?
## Installation
To get started fetch the MPTCP Linux kernel version used as the base for the patch set (here version v0.90):  
`$ git clone git://github.com/multipath-tcp/mptcp`  
`$ cd mptcp`  
`$ git checkout tags/v0.90`

Next, check out the patch files (or download them directly). Then copy them in the mptcp kernel folder and overwrite the original files.

Then, you need to compile and install the modified kernel. 

## Enabling FUSO
FUSO is turned off by default. To enable it:  
`sysctl net.mptcp.mptcp_rmt=1`  
`sysctl net.mptcp.mptcp_rmt_path_selection=2`  
FUSO was called RMT at our early stage of implementation. We have implemented two path selection mechanisms for FUSO's multi-path loss recovery. It has been shown that the second one performs better.

### A note on MPTCP
Note that you should first turn on MPTCP in order to use FUSO. How to configure MPTCP can be found [here](http://multipath-tcp.org/pmwiki.php/Users/ConfigureMPTCP).

We have made a minor optimization for the original MPTCP receiving end. Enabling this feature can further improve FUSO's performance. To enable the receiver optimization:  
`sysctl net.mptcp.mptcp_receive_ofo_optimize=1`
