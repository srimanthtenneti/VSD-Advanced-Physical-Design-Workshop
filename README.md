# VSD-Advanced-Physical-Design-Workshop
This workshop aims to give an idea on Physical Design using the 130nm Google Skywater PDK. This is a 5 day workshop focusing on various aspects of physical design. 
![Screenshot](Images/apd.png)
## Table of Contents
### 1. Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK
    1.How to talk to computers
    2.SoC design and OpenLANE
    3.Starting RISC-V SoC Reference design
    4.Get familiar to open-source EDA tools
### 2. Day 2: Understand importance of good floorplan vs bad floorplan and introduction to library cells
    1.Chip Floor planning considerations
    2.Library Binding and Placement
    3.Cell design and characterization flows
    4.General timing characterization parameters
### 3. Day 3: Design and characterize one library cell using Magic Layout tool and ngspice
    1.Labs for CMOS inverter ngspice simulations
    2.Inception of Layout – CMOS fabrication process
    3.Sky130 Tech File Labs
### 4. Day 4: Pre-layout timing analysis and importance of good clock tree
    1.Timing modelling using delay tables
    2.Timing analysis with ideal clocks using openSTA
    3.Clock tree synthesis TritonCTS and signal integrity
    4.Timing analysis with real clocks using openSTA
### 5. Day 5: Final steps for RTL2GDS
    1.Routing and design rule check (DRC)
    2.PNR interactive flow tutorial

## Tools used in the workshop
    1.Yosys – for Synthesis
    2.Magic – for Layout and Floorplanning
    3.CTS - TritonCTS - Synthesizes the clock distribution network
    4.NgSpice - for Characterisation
    5.OpenSTA – Pre-layout and Post-layout Static timing analysis
    
## Day 1 : Inception of open-source EDA, OpenLANE and Sky130 PDK
#### Introduction to the files
1. Skywater-pdk – Contains all the foundry provided PDK related files
2. Open_pdks – Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility
3. Sky130A – The open-source compatible PDK files
#### Activating Open Lane & Preparing design

##### Running Openlane
    ./flow.tcl is the script which runs the OpenLANE flow and -interactive starts the flow in the interactive mode. 
##### Preparing design
    prep -design picorv32a
![Screenshot](Images/prepdesign.png)

#### Running synthesis
    run_synthesis command synthesizes the design
![Screenshot](Images/Synth.png)

## Day 2: Understand importance of good floorplan vs bad floorplan and introduction to library cells
In the floor planning stage we set some parameters and place plan the area of the chip. The parameters we typically set are :

    1. Die Area : The area of the chip
    2. Core Area : Area for all the circutry
    3. Core Utilization : It is the ratio of area of netlist to area of the core
    4. Aspect Ratio : It is the ratio of width to height
    5. Pre-placed Cells : These IP blocks have user defined locations and are placed in the chip before place and route.
    6. Place i/o pins :  This is to use the netlist to determine where a specific pin should be placed
    7. Power Distribution Network : This is very important to ensure all the components get enough power to function properly
    
#### Running the floorplan
    run_floorplan is the command to run the floor plan
![Screenshot](Images/fp1.png)
#### Viewing the floorplan
We use the Magic tool to view the floorplan and for us to view it in magic we need 3 files:
1. Magic Tech file : sky130A.tech
2. LEF file : merged.lef
3. Def file of floorplan : picorv32a.floorplan.def

        magic -T <location of techfile> lef read <loction of lef file> def read <location of floorplan def file>
The above command can be used to view the floorplan in the Magic tool.

![Screenshot](Images/fdp.png)

#### Running the Placement
    run_placement command is used to run the placement 
![Screenshot](Images/floorplan.png)

 Also I did a small experiment with the parameters to look at the difference in placement. The above one is the design with all the default parameters and the one below is the design with the parameters prescribed in the workshop.

![Screenshot](Images/18.png)
