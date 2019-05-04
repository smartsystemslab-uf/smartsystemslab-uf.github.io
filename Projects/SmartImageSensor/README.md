<p align="right">
<a href="https://tjlw.github.io/">Go to Home page</a>
</p>




# Bio-Inspired Reconfigurable Neuromorphic Image Sensor



## Description

Cameras are pervasively used for applications like surveillance, traffic monitoring, and precision agriculture. Most camera systems, however, are used as data collection and relaying units while the processing happens at backend servers. This project focuses on bringing the processing units close to the image sensor to introduce parallelism in the design with the help of three types of processor namely pixel processor, region processor, and sequential processor. This architecture has three logical layers where those processors are distributed. Pixel-processors are distributed in the first logical layer of the digital pixel sensor (DPS), and there is a processor dedicated for each pixel. They work in parallel, handle low-level image processing applications, remove temporal redundancy in an image, and provide pixel-level parallelism. The second logical layer is comprised of a certain number of region-processors. A certain number of the pixel-processors form a group or region and the design has a region-processor for every region. Like pixel-processors, they also work in parallel, take input from the corresponding region to perform mid-\high-level image processing, remove spatial redundancy, and ensures region level parallelism. Those two layers jointly provide massive parallelism in the design. Finally, a sequential processor who resides in the last layer receives the extracted information from the region processors through a bus and complete the remaining task (high-level reasoning operations) to complete machine vision application. All those processors maintain hierarchical connections among the computational layers and reduce data volume through hierarchical processing. Moreover, those processors are reconfigurable in ASIC paradigm to handle different machine vision applications. This flexible design emulates some of the concepts of the biological vision system. The simulation result shows the processing archives high acceleration in vision application and saves a significant amount of power through the hierarchical processing.

<p align="center"> <img width="640" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Projects/SmartImageSensor/Images/hierarchy.jpg?raw=True"/> </p>
<p align="center">
	Block Diagram of the Computational Units in the Image Sensor
</p>

### Keywords

Inter-pixel Processing, image sensor, Image processing, VLSI, FPGA, ASIC, Bio-Inspired processing, Neuromorphic Computing.


### Evaluation Platform 

We implement the full RTL-to-GDSII flow on Application Specific Integrated Circuit (ASIC) for the Image Sensor at the block level using 1.1 V supply voltage and 800 MHz clock frequency in 45 nm technology. We used Synopsys VCS and Design Compiler to convert RTL to gate-level net-list, Cadence Innovus to Place and Route of the synthesized net-list, Cadence Calibre to check DRC violation, and finally Synopsys Primetime for Static Timing Analysis using Nangate library as process design kit (PDK). Besides, to evaluate the performance, we also implement the design on the FPGA board provided by Xilinx (Kintex Ultra scale plus evaluation board) using Vivado design suite 18.2. While using the FPGA, we concentrate on the RTL design which also implementable on the ASIC platform.   

## Goal of the Hierarchical Processing

The ultimate goal of the project is to truncate the redundant information to accelerate the machine vision application. The figure illustrated below gives the understanding of extracting the relevant information from an image and which makes event-driven processing.

<p align="center"> <img width="640" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Projects/SmartImageSensor/Images/MDPIJournal-Page-1.jpg?raw=True"/> </p>

Comparison of frame-based and event-based processing for a scene with three objects is presented in the figure above. The object 1 is a bird sitting on a branch which is on the top right corner of the image. The object 2 contains some insignificant scattered moving objects. Lastly, the object 3 is a flying bird who is flying in a serpentine way. In the frame based processing on the left, each frame is produced after executing each pixel and the frames are produced after a sudden time interval. Conversely, in our event-driven processing system, on the right, responds if there is a significant event. Here the processing for object 1 is discarded since there is no temporal change. Though the Object 2 has temporal change but it does not carry relevant information. Only object 3 has not redundant information and it is our target to perform processing on the serpentine path of the object 3 as shown in this figure.

### Overall Benifit of the Project

- The integration of several computational layer in the sensor provides in-sensor processing and brings the computational unit close to image sensor
- Pixel-Parallel design gives the bebefit of parallel processing and exhibits high acceleration of low/mid-level applications in the machine vision application.
- Bio-inspired Computing removes the temporal and spatial redundancy and it saves significant power and evergy in the hierarchical layers. Parallelly, the computing system reduces the data volume in each layer and it reduces the burden to the external sequential processor and accelerates the sequential operation in the vision application.
- The processors in each layer are reconfigurable to different application in ASIC. This allows flexibility in the design and enables us to apply the sensor for different application. 

