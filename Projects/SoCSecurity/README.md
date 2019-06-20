<p align="right">
<a href="https://smartsystemslab-uf.github.io">Home</a> | <a href="https://smartsystemslab-uf.github.io/Projects/">Projects</a>
</p>

# Project Name: System-on-Chip Security

## Overview of the project:
Security has become one of the most crucial parts of System-on-chip (SoC) design because of its usage in the internet of things (IoT) devices, cyber-physical systems, and embedded computing systems. The ever-increasing complexity of on-chip components and long supply chain make SoCs vulnerable to hardware and software attacks. These attacks can be originated either from inside the chip or from malicious software components. The 3rd party Intellectual Properties (IPs)  are becoming non-trusted because of the possibility of hardware trojans integrated inside the IP. Our proposed hardware sandbox which is briefly described in project 1 aims to safely integrate those non-trusted IPs in SoCs. Project 2 describes the automatic generation of hardware sandbox. In project 3, we consider software originated attacks to the hardware accelerator IPs and it’s mitigation techniques. 


## Hardware Sandbox: 
The goal of this project is the secure operation of non-trusted IPs in SoC. Figure 1 shows the proposed high-level structure of the hardware sandbox. The structure is designed to support the following security policies: Isolation policy that limits the IP to only allowable interactions, Containment policy that minimizes the damage caused by a malicious component, and Integrity policy that enforces authorized data accessibility and modifications. These policies are implemented through two distinct but complementary mechanisms: Complete Mediation, and Resources Virtualization. The “Checker" component implements the Complete Mediation mechanism by checking every interaction made by the user IP to the system and only authorizing allowable interactions as specified by the IP interface specification. The “Sandbox controller" implements the Resources Virtualization mechanism by providing virtual memory buffers (local to the user IP) and virtual IO access. It also generates a “virtual resources controller" in case there are more virtual resources competing for a single physical resource. “Status registers" are used to monitor and log the user IP security status. This is useful in that a subverted IP can’t launch a denial-of-service attack by repeatedly making illegal requests. Also, this can be used to log the user IP if it triggers a Trojan at run-time. This information can then be used to blacklist some vendors from the integrator’s list of contractors.
 
<p align="center"> <img height ="290" width="300" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Sujan05-patch-1/Projects/SoCSecurity/Images/Sandbox.jpg"/> </p>
<pre align="center">
	Figure 1: Block Diagram of Hardware Sandbox
</pre>

## Component Authentication Process for Sandboxed Layouts (CAPSL):
We developed a tool for automatic generation of hardware sandboxes, introduced in [1] for suspicious IPs. We address IP verification with the use of sandboxing to provide system protection from suspicious IPs with the use of behavioral monitors to detect illegal interactions and isolate possible damage with physical separation and virtualized resources. The CAPSL design flow develops a formal model of an IP’s interactions at its interface to generate the necessary elements to securely wrap the IP for integration into a trusted system. We capture the overall behavior of an IP from configuration files specifying interface information (connections and behavior), illegal actions, and system resource requirements. We capture component interactions with the interface automata (IA), while proposing a subset of the Properties Specification Language (PSL) and sequential extended regular expressions (SERE) for defining unauthorized behavior. Each element of the sandbox can be output as a design file of the same format (VHDL, SystemC, etc) as the system in which they are to be integrated.

<p align="center"> <img height ="240" width="420" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Sujan05-patch-1/Projects/SoCSecurity/Images/CAPSL.png"/> </p>
<pre align="center">
	Figure 2: Steps followed by CAPSL to generate hardware sandbox
</pre>

The GitHub link of CAPSL tool is given below. 

https://smartes.uark.edu/project/capsl/


## Flask Security Architecture in SoC:
Accessing custom hardware IPs in FPGA accelerated SoCs are not controlled by the Operating system. Hence, there is a possibility of confidential information leakage and denial of service attacks on those IPs. In this project, we propose a hardware isolation approach to ensure controlled access to hardware IPs in the FPGA part of an SoC. The figure describes the architecture of our proposed FPGA accelerated secured embedded system. The access to an IP is enforced through the Access Control Unit (HMM) which is a hardware-software co-design and work with the Flask security architecture (described in the figure) integrated into the operating system. The benefit of using this security framework is less area overhead and can be easily integrated into the system.


<p > 
	<img align="center" height ="220" width="440" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Sujan05-patch-1/Projects/SoCSecurity/Images/HACU.png"/> 
	<img align="right" height ="220" width="300" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/Sujan05-patch-1/Projects/SoCSecurity/Images/Flask_archirectire.png"/>
</p>


<pre>
     Figure 3: Secured SoC Architecture with HACU                Figure 4: Flask Security Architecture
</pre>

### Publications
- Christophe Bobda, Joshua Mead, Taylor JL Whitaker, Charles Kamhoua, and Kevin Kwiat. "Hardware sandboxing: A novel defense paradigm against hardware trojans in systems on chip." In International Symposium on Applied Reconfigurable Computing, pp. 47-59. Springer, Cham, 2017.
- Festus Hategekimana, Taylor Whitaker, Md Jubaer Hossain Pantho, and Christophe Bobda. "Shielding non-trusted IPs in SoCs." In 2017 27th International Conference on Field Programmable Logic and Applications (FPL), pp. 1-4. IEEE, 2017.
- Festus Hategekimana, Taylor JL Whitaker, Md Jubaer Hossain Pantho, and Christophe Bobda. "Secure integration of non-trusted IPs in SoCs." In 2017 Asian Hardware Oriented Security and Trust Symposium (AsianHOST), pp. 103-108. IEEE, 2017.
- Festus Hategekimana, and Christophe Bobda. "Applying the Flask Security Architecture to Secure SoC Design." In 2017 IEEE 25th Annual International Symposium on Field-Programmable Custom Computing Machines (FCCM), pp. 198-198. IEEE, 2017.
- Festus Hategekimana, Joel Mandebi Mbongue, Md Jubaer Hossain Pantho, and Christophe Bobda. "Inheriting Software Security Policies within Hardware IP Components." In 2018 IEEE 26th Annual International Symposium on Field-Programmable Custom Computing Machines (FCCM), pp. 53-56. IEEE, 2018.
