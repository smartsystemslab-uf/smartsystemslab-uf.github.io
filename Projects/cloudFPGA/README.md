<p align="right">
<a href="https://smartsystemslab-uf.github.io">Home</a> | <a href="https://smartsystemslab-uf.github.io/Projects/">Projects</a>
</p>



# FPGA Virtualization in Cloud Infrastructures


## Description
Cloud computing has become the major trend for delivering services via networks. The overall global public cloud market has known an increasing growth in recent years. Reports for the end of 2017 placed the value of the global cloud market at $246.8 billion compared to $209.2 billion in 2016 [1]. One of the reasons of its success is that it allows privates and companies to access computing and storage resources on demand without having to care about the management of the underlying infrastructure. Consumers are now freed from some considerations like the acquisition and maintenance of computing infrastructures, and the power consumption monitoring. Major IT and Web companies (Microsoft, Oracle, IBM, Amazon, Google, …) have all proposed cloud solutions (AWS, Google Compute Engine, ExaData, …). The architectures underneath those cloud services mostly rely on General Purpose Processors (GPP). Heterogeneous paradigms are well known to offer greater advantages compared to general purpose computing such as performance improvement and power savings. Knowing that specialized units like Graphics Processing Units (GPUs) and reconfigurable processors such as FPGAs outperform GPP in many applications, finding an efficient way to incorporate such computing resources into today’s and tomorrow’s cloud architectures might open a new era for cloud computing. Specifically, the purpose of this work is to investigate the integration of FPGAs into cloud infrastructures.

## Contribution

Virtualization techniques can be categorized as software-based approaches and hardware-based ones. Emulation and paravirtualization fall into the software-based category. For the first one, the hypervisor emulates hardware devices (see Figure 1a). VMs can then use native drivers, resulting in no modification of guest operating systems (GOS). The major drawback is the overhead of context switches between GOS and host operating systems (HOS). Paravirtualization (see Figure 1b) offers a more efficient scheme as a front-end driver in the VM is connected
to a back-end driver in the host to remove context switches’ overhead. The two previous methods insert a hypervisor between VMs and the hardware, introducing penalties in VM I/O performance. Hardware-based virtualization techniques aim to mitigate that overhead. Direct I/O (see Figure 1c) gives VMs a direct access to physical hardware, resulting in improved performance compared to previously mentioned methods. Unfortunately, this approach does allow sharing physical devices among VMs, which is one of the most important requirement to virtualizing hardware in the cloud. Specifications like Single Root I/O Virtualization (SR-IOV) allow multiple VMs to access the same physical device (see
Figure 1d). It features several Physical Functions (PF), each accessible through Virtual Functions (VF). Each VM can directly reach a VF to achieve bare metal performance [2]. Though the latter offers some sharing capability, each VF can only be accessed by one VM, making this approach not scalable in a cloud-oriented deployment. <b> We therefore propose a paravirtualized virtio-based framework that opens communication channels between VMs and FPGAs. Further, we design an FPGA overlay featuring VFs purposed to run guest’s hardware tasks by leveraging partial reconfiguration (PR).</b>

<p align="center"> <img width="400" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Mandebi/Projects/cloudFPGA/Images/virtualizationApproaches.png?raw=True"/> </p>
<p align="center">
	Figure 1. Virtualization Approaches
</p>


## Overall Framework
The framework is a hardware/software architecture that relies on Virtio-vsock for communication between VMs and FPGAs. Virtual machines are connected with the hypervisor through unix-based sockets with a context identifier (CID) and a port number. Figure 2 highlights its major components and operation. The <i>FPGA Management Service</i> controls the access to the physical FPGA. It uses the <i>CID/VF Mapping Table</i> to keep track of FPGA regions assigned to VMs. The FPGA mainly contains an overlay architecture provisioning VFs to VMs, and a set of Block RAMs (BRAMs) to store VFs’ data. FPGA resources being finite, VFs are designed with a specific size. This implies that each design provided by users should match that size requirement. Users will therefore split designs which are bigger than a VF into smaller hardware tasks, and request additional VFs. The overlay architecture makes it possible to assign several VFs on the same FPGA or on distant ones to a user. This allows to meet the availability requirement for cloud services as hardware tasks belonging to a user can be distributed over several FPGAs. Upon assigning a VF to a VM, the FPGA Management Service updates the <i>CID/VF Mapping Table</i> with the goal of recording the FPGA usage.


<p align="center"> <img width="400" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Mandebi/Projects/cloudFPGA/Images/overallFramework.png?raw=True"/> </p>
<p align="center">
	Figure 2. Framework Components
</p>

## Experimental Observation

### Testing Platform
For testing purposes, we implemented the proposed architecture on an Hybrid Memory Cube server from Micron running CentOS-7 with a kernel of version 4.10.0. It was equipped with an Intel Core i7-5930K CPU embedding 12 cores of frequency 3.50GHz. The server had 32GB of RAM, and we used QEMU version 2.11.50 for emulating VMs. Each VM was running an Ubuntu 16.04.01 operating system with 4GB of RAM. We implemented the FPGA overlay in VHDL on a Xilinx Kintex Ultrascale XCKU060-ffva1156-2-e FPGA using Vivado Lab Edition 2015.4. The FPGA board was attached to the motherboard of the server through a PCIe Gen3 ×16 connector. Finally, we utilized the Pico API version 6.0.0.21 for packet exchange between FPGAs and HOS.

### Preliminary Results
Figure 3 examines how the bandwidth scales with the number of VMs running. Typically, the bandwidth diminishes as we increase the number of VMs. This is simply a resultant of several VMs trying to transfer payloads of different sizes to their VFs simultaneously.
<p align="center"> <img width="400" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Mandebi/Projects/cloudFPGA/Images/bandwidth.png?raw=True"/> </p>
<p align="center">
	Figure 3. Bandwidth Study
</p>
The bandwidth goes down from about 5GB/s with one VM (running on 1 CPU) to 2.3GB/s with four VMs (running on 2 CPUs each) for 64KB payloads. It is also observed that smaller payloads does not significantly influence the average bandwidth independently of the number of VMs or virtual CPU cores (additional details are found in publications (1) and (2)).


## References
[1] Gartner, “Gartner Says Worldwide Public Cloud Services Market to Grow 18 Percent in 2017”, Gartner, Inc, 2017. <br>
[2] Zhang, Binbin, Xiaolin Wang, Rongfeng Lai, Liang Yang, Yingwei Luo, Xiaoming Li, and Zhenlin Wang. "A survey on i/o virtualization and optimization." In 2010 Fifth Annual ChinaGrid Conference, pp. 117-123. IEEE, 2010.


## Publications
1- Mandebi Mbongue, Joel, Danielle Tchuinkou Kwadjo, and Christophe Bobda. "Flexitask: A flexible fpga overlay for efficient multitasking." In Proceedings of the 2018 on Great Lakes Symposium on VLSI, pp. 483-486. ACM, 2018. <br><br>
2- Mbongue, Joel, Festus Hategekimana, Danielle Tchuinkou Kwadjo, David Andrews, and Christophe Bobda. "FPGAVirt: A Novel Virtualization Framework for FPGAs in the Cloud." In 2018 IEEE 11th International Conference on Cloud Computing (CLOUD), pp. 862-865. IEEE, 2018. <br><br>
3- Mbongue, Joel Mandebi, Festus Hategekimana, Danielle Tchuinkou Kwadjo, and Christophe Bobda. "FPGA Virtualization in Cloud-Based Infrastructures Over Virtio." In 2018 IEEE 36th International Conference on Computer Design (ICCD), pp. 242-245. IEEE, 2018. <br>

## Future Work
 <ul>  
  <li> Extend the virtualization environment to handle more virtual machines </li>
  <li> Study security threats arising from sharing FPGA resources between multiple tenants </li>  
</ul>

## Contact
<ul>
    <li> <a href="https://www.linkedin.com/in/joel-mandebi-77123641/">Joel Mandebi Mbongue (jmandebimbongue@ufl.edu)</a> 
    <li> <a href="http://bobda.ece.ufl.edu/">Dr Christophe Bobda  (cbobda@ece.ufl.edu)</a> 
</ul>
