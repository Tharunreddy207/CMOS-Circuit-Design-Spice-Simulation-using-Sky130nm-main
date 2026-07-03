# CMOS-Circuit-Design-Spice-Simulation-using-Sky130nm-technology
## NgspiceSky130-Day1-Basics of NMOS Drain Current(Id) vs Drain-to-source Voltage(Vds)

### Introduction to Circuit Design and Spice Simulations

#### L1 Why do we need SPICE simulations?
![alt text](<Screenshot 2026-07-02 125156.png>)
what is circuit design? Circuit design is basically designing a circuit which can give the required output such as NAND,NOR etc 
![alt text](<Screenshot 2026-07-02 125122.png>)
We need SPICE simulation to test if our designed circuit is working or not ,we can simulate the circuit,plot the characterstics and get the delay table
![alt text](<Screenshot 2026-07-02 125454.png>)
![alt text](<Screenshot 2026-07-02 125610.png>)
After the SPICE simulation we obtain a delay table which is an important aspect in designing circuits

#### L2 Introduction to basic element in circuit design-NMOS
![alt text](<Screenshot 2026-07-02 130410.png>)
A MOSFET is 4 terminal voltage controlled device.It contains of substrate(here P type),two hughky doped diffusion regions N+ they are Source and Drain.There is a SiO2 layer above which is the gate terminal
![alt text](<Screenshot 2026-07-02 130344.png>)
When Vgs is 0V All the other terimnals are gorunded and the substrate-source and substrate-drain form two P-N junctions which have not recieved the requireed bias voltage.This forms a high resistance path between the s-d

#### L3 Strong inversion and threshold voltage
![alt text](<Screenshot 2026-07-02 130344-1.png>)
When Vgs is given a +ve voltage the negative charges starts accumulating at the ned of the oxide layer 
![alt text](<Screenshot 2026-07-02 131331.png>)
when further Vgs is increased then a phenonmenon named "Surface inversion" happens.The Vgs at which surface inversion occurs is called Vth
When Vgs is increases even after the Vth is reached then the electrons from the source and drain come nearer and form a channel.But as there is no Vds voltage there is no current between source and drain this region is called "CUT-OFF" region
![alt text](<Screenshot 2026-07-02 131901.png>)
As Vss (the voltage between source and substrate is increased) the depletion layer near the source is incrases in width

#### L4 Threshold voltage with positive substrate potential
![alt text](<Screenshot 2026-07-02 132458.png>)
Due to this Vss surface inversion will be slower and needs more Vth to occur.The new Vth formula is as given above
![alt text](image.png)
Here the parameters such as gamma are given by the foundaries which will be used in the spice simulation

### NMOS resistive region and Saturation region of operation
#### L1 Resistive region of operation with small drain-source voltage
![alt text](<Screenshot 2026-07-02 134956.png>)
what happens Vds is increases when Vgs>Vth.this induces a current between source and drain called the drain current.The induced charge in the channel is proportional to Vgs-Vth

#### L2 Drift current theory
![alt text](<Screenshot 2026-07-02 160925.png>)
The channel voltage at any point x is Vgs-Vth-V(x)where yaxis represents the width of MOS xaxis is the voltage across the channel.
![alt text](<Screenshot 2026-07-02 161406.png>)
There are two currents inside the channel diffusion and drift.Diffusion current is due to the difference in charge concentration and is very small.Drift current is current due to Vds 

#### L3 Drain current model for Linear region of operation
![alt text](<Screenshot 2026-07-02 161919.png>)
When we integrate dx over 0 to L and dV from 0 to Vds we get the id equation
The obtained id equaation is for linear region where Vds lesserthan Vgs-Vth

#### L4 SPICE conclusion to resistive operation
![alt text](<Screenshot 2026-07-02 162655.png>)
To know whether the device is in linear region or not and also to know the id value we need to sweep the value of Vds over 0 to Vgs-Vth and calculate id which can be done in SPICE simulation

#### L5 Pinch-off region condition
![alt text](<Screenshot 2026-07-02 163010.png>)
Now when Vds is increased keeping Vgs constant, we make a table comparing Vgs-Vds with Vth. The MOS device will stay in linear region untill Vgs-Vds is greater than Vth
![alt text](<Screenshot 2026-07-02 163150.png>)
when Vgs-Vds=Vth then  there is no more surface inversion after this point where channel volltage is Vth.This is called pinch-off condition where Vds=Vgs-Vth
![alt text](<Screenshot 2026-07-02 163308.png>)
When Vds is increased further the channel near the drain disappears.Now this region is called SATURATION Region(Vds>Vgs-Vth) where current id cannot increase further

#### L6 Drain current model for saturation region of operation
![alt text](<Screenshot 2026-07-02 163610.png>)
The id current saturates as said before therefore the curernt equation changes to the above one
![alt text](<Screenshot 2026-07-02 163736.png>)
As Vds is further increases the current must be constant ideally but as the effective channel length is decreasign this introduces a new effect called channle length modulation(lambda)

### Introduction to SPICE
#### L1 Basic SPICE setup
![alt text](<Screenshot 2026-07-02 165449.png>)
These parameters are directly given from the foundaries and must be fed into the SPICE engine
![alt text](<Screenshot 2026-07-02 165617.png>)

#### L2 Circuit description in SPICE syntax
![alt text](<Screenshot 2026-07-02 165759.png>)
We must define the nodes and name them
![alt text](<Screenshot 2026-07-02 170001.png>)
The syntax to define a mosfet as it is a 4 terminal device we use the mosfet_name drain gate source substrate techonology_file W=value L=value
![alt text](<Screenshot 2026-07-02 170221.png>)
resistor is two termnial device so its just resistor_name node1 node2 value
![alt text](<Screenshot 2026-07-02 170346.png>)
This is the entire syntax for a small mos circuit

#### L3 Define Technology parameters
![alt text](<Screenshot 2026-07-02 171024.png>)
The model name for NMOS is give above which contains all the parameters highlighted in the right side 
![alt text](<Screenshot 2026-07-02 171145.png>)
To access the required technology file we must include the packaged file

#### L4 First SPICE simulation
Open Virtual box
Type cd
git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
type cd sky130CircuitDesignWorkshop/Design/
![alt text](<Screenshot 2026-07-02 171729.png>)
![alt text](<Screenshot 2026-07-02 171959.png>)
Open the cells directory and we can find all the nfet and pfet packaged file and all the techonology parameters required for each and every mosfet we will be using in this course
![alt text](<Screenshot 2026-07-02 172126.png>)
In desgin folder open the day1.spie file
![alt text](<Screenshot 2026-07-02 172318.png>)
We can see the W,L values and the entire netlist
![alt text](<Screenshot 2026-07-02 172425.png>)
Now run the day1.spice file and plot -vdd#branch
![alt text](<Screenshot 2026-07-02 172511.png>)
This is id vs Vds graph for the circuit 

#### L5 SPICE lab with Sky130 models
![alt text](<Screenshot 2026-07-02 173308.png>)
open the cells and see that  W and L values are in microns.

## NgspiceSky130-Day2-Velocity saturation and basics of CMOS inverter VTC
### SPICE simulation for lower nodes and velocity saturation effect
#### L1 SPICE simulation for lower nodes
![alt text](<Screenshot 2026-07-02 173700.png>)
The graph for id vs Vds tells about the 3 regions,to the left of the blue line it is linear region and to the right is saturation and the region where id is almost 0 is the cutoff region
![alt text](<Screenshot 2026-07-02 173935.png>)
Now we will try plotting for different device with W=0.375u and L=0.25u but the ration remaining the same

#### L2 Drain current vs gate voltage for long and short channel device
![alt text](<Screenshot 2026-07-02 174032.png>)
![alt text](<Screenshot 2026-07-02 174424.png>)
![alt text](<Screenshot 2026-07-02 174511.png>)
In the longer MOS we see that there is quadratic dependence of id on Vgs-Vth but ther shorter MOS has only linear dependence
![alt text](<Screenshot 2026-07-02 175008.png>)
Now keeping the Vds constant we will sweep Vgs and plot id vs Vgs 
![alt text](<Screenshot 2026-07-02 175226.png>)
The obtained ids vs Vgs for both devices confirm the above made observation

#### L3 Velocity saturation at lower and higher electric fields
![alt text](<Screenshot 2026-07-02 175640.png>)
The above photo shows us what Velocity saturation is at Electric fields higher than the critical electriv field the velocity of electrons in the channel is saturated and cannot increase further 
![alt text](<Screenshot 2026-07-02 175938.png>)
This effect introduces one more mode of operation Velocity saturation mode.The new id equation becomes as shows in the figure
Now id depends on the minimum of (Vdsat,Vgs-Vth,Vds)
![alt text](<Screenshot 2026-07-02 180518.png>)
![alt text](<Screenshot 2026-07-02 180611.png>)
![alt text](<Screenshot 2026-07-02 180710.png>)
Here id is inversely proportional to L but this is mot the case practically
![alt text](<Screenshot 2026-07-02 180940.png>)
The peak current of the shorter MOS is lesser than the peak current of longer MOS

#### L5 Labs Sky130 Id-Vgs
![alt text](<Screenshot 2026-07-02 181300.png>)
open the day2.spice
![alt text](<Screenshot 2026-07-02 181357.png>)
Run the day2.spice file and plot -vdd#branch
![alt text](<Screenshot 2026-07-02 181540.png>)
id vs Vds graph
![alt text](<Screenshot 2026-07-02 181954.png>)
id vs Vgs graph

#### L6 Labs Sky130 Vt
![alt text](<Screenshot 2026-07-02 181954.png>)
Using the Id vs Vgs graph we can obtain Vth click on the point shown in the figure and we obtain the Vth show below
![alt text](image-1.png)

### CMOS voltage transfer characteristics (VTC)
#### L1 MOSFET as a switch
![alt text](<Screenshot 2026-07-02 213959.png>)
When Vgs is greatre than Vth then the MOS acts as a closed circuit and as an open circuit when Vgs is lesser than Vth 
![alt text](<Screenshot 2026-07-02 214201.png>)

#### L2 Introduction to standard MOS voltage current parameters
![alt text](<Screenshot 2026-07-02 214438.png>)
When Vin is high (Vdd) only NMOS is turned ON and when Vin is low only PMOS is turned ON
![alt text](<Screenshot 2026-07-02 214656.png>)
When only NMOS is turned ON there is a current path from capacitor to Rn(through NMOS) to gnd and there is direct path from Vdd to ground through Rp(pmos) when onloy PMOS is ON And the value of id is same in both cases.
![alt text](<Screenshot 2026-07-02 214858.png>)

#### L3 PMOS/NMOS drain current vs drain voltage
![alt text](<Screenshot 2026-07-02 215148.png>)
By observation we write the above equations
![alt text](<Screenshot 2026-07-02 215239.png>)
Also we know that idn vs Vdsn graphs

#### L4 Step1- Convert PMOS gate-source-voltage to Vin
![alt text](<Screenshot 2026-07-02 215547.png>)
considering only PMOS we get the above table with keeping constant Vdd and changing the Vgsp
![alt text](<Screenshot 2026-07-02 215622.png>)
The idsp vs Vdsp graph is now plotted as idsn vs -Vdsp as shown above

#### L5 Step2 & Step3- Convert PMOS and NMOS drain-source-voltage to Vout
![alt text](<Screenshot 2026-07-02 215944.png>)
The obtained idN vs -Vdsp is converted to idn vs Vout by using the equation Vout is Vdd+Vdsp
This is called "LOAD CURVE OF TRANSISTOR"
Now repeat the same procedure for NMOS
#### L6 Step4- Merge PMOS-NMOS load curves and plot VTC
![alt text](<Screenshot 2026-07-02 220237.png>)
![alt text](<Screenshot 2026-07-02 220247.png>)
![alt text](<Screenshot 2026-07-02 220410.png>)
We have now obtained the NMOS load curve
![alt text](<Screenshot 2026-07-02 220620.png>)
We need to superimpose Load curve of both transistors to obtain VTC
![alt text](<Screenshot 2026-07-02 220656.png>)

## NgspiceSky130-Day3-CMOS switching threshold and dynamic simulations
### Voltage transfer characteristics-SPICE simulations
#### L1 SPICE deck creation for CMOS inverter
![alt text](<Screenshot 2026-07-02 221325.png>)
For the spice deck we need to decide on the above 4 things 
![alt text](<Screenshot 2026-07-02 221519.png>)

#### L2 SPICE simulation for CMOS inverter
![alt text](<Screenshot 2026-07-02 221800.png>)
This is the netlist that we have written
![alt text](<Screenshot 2026-07-02 222130.png>)
The above is Vout vs Vin plot for Wn=Wp=0.375u, Ln=Lp=0.25u, Wn/ln=Wp/Lp=1.5
![alt text](<Screenshot 2026-07-02 222330.png>)
The above is Vout vs Vin plot for Wn= 0.375u, Wp= 0.9375u, Ln,p=0.25u; Wn/Ln=1.5, Wp/Lp=2.5
The graph is shifted to the right as we can see

#### L3 Labs Sky130 SPICE simulation for CMOS
Following the previous instruction we run day3.spice
![alt text](<Screenshot 2026-07-02 222542.png>)
![alt text](<Screenshot 2026-07-02 222657.png>)
![alt text](<Screenshot 2026-07-02 222817.png>) 
When we zoom into the point where Vin=Vout we get Vm 
Now run the trans file in day3.spice
![alt text](<Screenshot 2026-07-02 222958.png>)
![alt text](<Screenshot 2026-07-02 223051.png>)
Zoom in part where Vout is falling and get two points
![alt text](<Screenshot 2026-07-02 223208.png>)
By subtracting the  x coardinates(time) we get RISE DELAY
![alt text](<Screenshot 2026-07-02 223257.png>)
Zoom in part where Vout is rising and get two points
![alt text](<Screenshot 2026-07-02 223343.png>)
By subtracting the  x coardinates(time) we get FALL DELAY

### Static behaviour evaluation-CMOS inverter robustness-Switching Threshold
#### L1 Switching Threshold, Vm
![alt text](<Screenshot 2026-07-02 224201.png>)
What is swithcing threshold?It is the point when Vin=Vout and the swithcing threshold has increased for the CMOS inverter with larger PMOS width
![alt text](<Screenshot 2026-07-02 224527.png>)

#### L2 Analytical expression of Vm as a function of (W/L)n and (W/L)p
![alt text](<Screenshot 2026-07-02 224716.png>)
Using the above equations we will find the expressions for Vm and W/L
![alt text](<Screenshot 2026-07-02 224755.png>)
The above is Vm written as a function of W/L


#### L3 Analytical expression of (W/L)n and (W/L)p as a function of Vm
![alt text](<Screenshot 2026-07-02 224936.png>)
Here W/L is written as a function of Vm

#### L4 Static and Dynamic simulation of CMOS inverter
now plotting Vout vs Vin and also finding out rise delay and fall delay for differnt ratios of (W/L)(p) and (W/L)(n)
![alt text](image-2.png)
![alt text](image-4.png)
![alt text](image-3.png)

#### L5 Static and Dynamic simulation of CMOS inverter with increased PMOS width
Now repeating the process for Pmos being twice the width of NMOS
![alt text](image-5.png)
![alt text](image-6.png)
 Pmos being twice the width of NMOS
![alt text](image-7.png)
 Pmos being thrice the width of NMOS
![alt text](image-8.png)
Pmos being 4times the width of NMOS
![alt text](image-9.png)
Pmos being 5times the width of NMOS
![alt text](image-10.png)
The final observation

#### L6 Applications of CMOS inverter in clock network and STA
Conclusions from the final observation seen
1)If there is some error in fabrication that will not affect the entire circuit because both Vm and delays increase or decrease in very small amount this shows the robustness of the cmos inverter
2)When PMOS is twice as wide as NMOS the rise and fall delay is almost the same this shows the symmetry of cmos inverter and this is used in clock inverter/buffer
![alt text](image-11.png)

## NgspiceSky130-Day4-CMOS Noise Margin robustness evaluation
### Static behaviour evaluation-CMOS inverter robustness-Noise Margin
#### L1 Introduction to Noise Margin
![alt text](image-12.png)
When we see the Vout vs Vin plots ideally it Vout must go to 0 when Vin is Vdd/2 with infinite slope
But practically Vout decreases gradually with finite slope and never reaches zero
![alt text](image-13.png)
We consider Vil as inpult low voltage and any voltage less than this is considered as logic 0
![alt text](image-14.png)
We conside Voh output high voltage any voltage higher than Voh and less than Vdd is logic 1
![alt text](image-15.png)
We consider Vih input high voltage any voltage higher than Vih and less than Vdd is logic 1
![alt text](image-16.png)
We consider Vol output low voltage any voltage lower than this is logic 0

#### L2 Noise Margin voltage paramters
we the above consdierations we obtain the below plot
![alt text](image-17.png)
The slope is -1 because Vout is decreasing and Vin is increasing 

#### L3 Noise margin equation and summary
![alt text](image-18.png)
This is the noise margin where the it is logic 1 when the voltage is between Voh and Vih and logic 0 when the voltage is between Vol and Vil
![alt text](image-19.png)

#### L4 Noise margin variation with respect to PMOS width
![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-22.png)
![alt text](image-23.png)
![alt text](image-24.png)
![alt text](image-25.png)
The Noise margins for different Pmos width was discussed 
![alt text](image-26.png)
![alt text](image-27.png)

#### L5 Sky130 Noise margin labs
Follow the same proecedure and run the day4.spice file
![alt text](image-28.png)
taking  W/L ratio of PMOS to NMOS = 2.77 and sweeping  Vin from 0 to 1.8V with step size of 0.01V
![alt text](image-29.png)
![alt text](image-30.png)
These are the points where slope is -1 
using this we can get the Nmh as 0.72 and Nml as 0.67

## NgspiceSky130-Day5-CMOS power supply and device variation robustness evaluation
### Static behaviour evaluation-CMOS inverter robustness-Power supply variation
#### L1 Smart SPICE simulations for power supply variations
![alt text](image-31.png)
For the above device we will simulate for varying Vdd (decreasing)
![alt text](image-32.png)
The above netlist has a small loop to change the Vdd
![alt text](image-33.png)

#### L2 Advantages and disadvantages using low supply voltage
we will discuss some advantages and disadvantages
![alt text](image-34.png)
gain factor is ratio of change in output to change in input

Two points in the curve is chosen and we take the slope of it 
Gain factor of one curve is shown below
![alt text](image-35.png)
![alt text](image-36.png)
![alt text](image-37.png)
![alt text](image-38.png)
![alt text](image-39.png)
As Vdd is decreased the gain factor increases

![alt text](image-40.png)
![alt text](image-41.png)

Disadvantages
The rise and fall delay increases which affects the perofomance
![alt text](image-42.png)
![alt text](image-43.png)
![alt text](image-44.png)

#### L3 Sky130 Supply variation Labs
![alt text](image-45.png)
Run day5.spice file 
![alt text](image-46.png)
![alt text](image-47.png)
Using these two coordinates we can calculate Gain

### Static behaviour evaluation-CMOS inverter robustness-Device variation
#### L1 Sources of variation - Etching process
![alt text](image-48.png)
A single CMOS inverter is shown how they are connected with other (by each other meaning the terminals of mos devices)
The shape of the terminals(here rectangle) depends on the etching process
![alt text](image-49.png)
Imgaine an inverter chain like the one above 
![alt text](image-50.png)
Due to some issues in etching there will be some errors in L and W of the device which causes error in the area
![alt text](image-51.png)
There is no significant change in the operation due to the middle devices as they have the cmos inverter in either side .The main issue in the operation will be caused by the first and last inverters
![alt text](image-52.png)

#### L2 Sources of variation - Oxide thickness
The next source of variation is oxide thickness
![alt text](image-53.png)
![alt text](image-54.png)
The oxide layer thickness will be affected by the oxidatin process,this varies our id 
![alt text](image-55.png)

#### L3 Smart SPICE simulation for device variations
![alt text](image-56.png)
We will now do some spice simulation for weak Nmos strong Pmos and also the vice versa 
![alt text](image-58.png)
![alt text](image-57.png)

#### L4 Conclusion
![alt text](image-59.png)
the stronger the PMOS and weaaker NMOS the graph shifts right increasing Vm 
Even when we plot the Vout vs Vin graphs for the waek and strong Pmos and Nmos inverters
We see that Vm,Nmh and Nml are decreasing but in very small amounts, so even if there are errors in the device fabrication or etching it will not cause issues
This again proves us that CMOS inverter is robust

![alt text](image-60.png)
The operation of cmos inveerter gate is still intact even after changing the power supply and device variations

#### L5 Sky130 device variations labs
![alt text](image-61.png)
clearly it is a strong PMOS and weak NMOS
![alt text](image-62.png)