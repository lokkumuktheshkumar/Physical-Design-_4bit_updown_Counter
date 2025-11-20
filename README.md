# Exp 5 Physical Design of a 4-Bit Up-Down Counter

## Aim:

Execute floorplanning, power planning, and placement for the synthesised 4-bit up-down counter design.

## Tool Required:

Physical Design: Innovus

## Mandatory Inputs for PD: 

1. Gate Level Netlist [Output of Synthesis]
   
2. Block Level SDC [Output of Synthesis]
   
3. Liberty Files (.lib)
   
4. LEF Files (Layer Exchange Format)
   
## Procedural Steps:

Ensure the Synthesis for the target design is complete, and then open a terminal from the corresponding workspace. 

• Initiate the Cadence tools and cmd:innovus (Press Enter) 

• For Innovus tool, a GUI opens, and the terminal also enters the Innovus command prompt, where the tool commands can be entered. 

After importing the Design, Perform the following Physical Design stages:

→ Floor Planning 

→ Power Planning

→ Placement
Note : Check the paths to properly read in the input files. 

•	Else, if you would like to import your design using GUI, open the Innovus tool and from the GUI, go to File → Import Design.

o	A new pop-up window appears. 

o	First, load the netlist. You can browse for the file and select “Top cell : Auto Assign”.

•	Similarly, select your LEF files from the specified path.

•	Once LEF Files are loaded, Next step is to create the power supply pins both VDD and VSS

•	In order to load the Liberty File and SDC, create delay corners and analysis view, select the “Create Analysis Configuration” option at the bottom.

o	An MMMC browser Pops Up.

<img width="819" height="670" alt="image" src="https://github.com/user-attachments/assets/12b66c0e-44d0-437e-878e-7620932e7edd" />

The order of adding the MMMC Objects is as follows. 

1. Library Sets
   
2. RC Corners
 
3. Delay Corners
   
4. Constraints (SDC)
   
Once all of them are added, Analysis Views are created and assigned to Setup and Hold. 

In order to add any of the objects, make a right click on the corresponding label → Select New. 

Adding Liberty Files (slow.lib, fast.lib) under “Library Sets

• add slow.lib with a label Slow or any identifier of your own.

### Fig.1 Add slow Library set

• add fast.lib with a label Fast or any identifier of your own.
<img width="1919" height="1130" alt="Screenshot 2025-11-19 152443" src="https://github.com/user-attachments/assets/08ea35fc-aa48-40f5-8ca3-2d8b67c8b27a" />

### Fig.2 Add fast Library set

• Adding RC Corners can also be done in a similar process. The temperature value can be found under the corresponding liberty file. Also, cap table and RC Tech files can be added from Foundry where available.
<img width="1919" height="1120" alt="Screenshot 2025-11-19 152538" src="https://github.com/user-attachments/assets/63ec3bcd-dd60-4daf-989c-d9c930a5e669" />

### Fig.3 Add RC corner

• Delay Corners are formed by combining Library Sets with RC Corners.
<img width="1917" height="1123" alt="Screenshot 2025-11-19 152830" src="https://github.com/user-attachments/assets/449a243b-6e00-4134-9c37-6c4b182a63d6" />

### Fig.4 Add Delay corner Max_delay & Min_delay

• Similarly, SDC can be read under the MMMC Object of “Constraints”.
<img width="1919" height="1135" alt="Screenshot 2025-11-19 152936" src="https://github.com/user-attachments/assets/ad195103-6392-4cc9-8756-514f52a270cd" />
<img width="1918" height="1128" alt="Screenshot 2025-11-19 153024" src="https://github.com/user-attachments/assets/eb988334-372e-4b3a-b78f-3f1b5f48f8d3" />

### Fig.5 SDC Constraint file

• Analysis Views are formed from combinations of SDC and Delay Corner.
<img width="1918" height="1131" alt="Screenshot 2025-11-19 153154" src="https://github.com/user-attachments/assets/52847ba9-8538-4ded-b9d5-ba52833d4d5d" />

### Fig.6 Add Analysis View Worstcase & Bestcase

• Once “Best” and “Worst” Analysis views are created, assign them to Setup and Hold.
<img width="1911" height="1140" alt="Screenshot 2025-11-19 153348" src="https://github.com/user-attachments/assets/f4e353c9-907d-4714-91f7-9fd302e87996" />
<img width="1915" height="1136" alt="Screenshot 2025-11-19 153406" src="https://github.com/user-attachments/assets/aa4aeb4f-8bd0-4e21-ad33-5a01aa1664a1" />

### Fig.7 Add Setup Analysis View & Hold Analysis View

• Once all the process is done, Click on “Save&Close” and save the script generated with any name of your choice. 

• Make sure the file extension remains .view or .tcl 

• After saving the script, go back to Import Design window and Click “OK” to load your design.

<img width="829" height="504" alt="image" src="https://github.com/user-attachments/assets/9daa96ae-ee07-42a3-804a-58f68763fd55" />

In the Import Design window click the save option to save the Default.globals file

• A rectangular or square box appears in your GUI if and only if all the inputs are read properly.
<img width="1919" height="1133" alt="Screenshot 2025-11-19 153445" src="https://github.com/user-attachments/assets/38631e38-8812-43e8-85cd-9a6a79c6d6ec" />
<img width="1918" height="1126" alt="Screenshot 2025-11-19 153500" src="https://github.com/user-attachments/assets/69524348-506d-4b47-98ac-e3c5fe5218f6" />
<img width="985" height="832" alt="Screenshot 2025-11-19 153511" src="https://github.com/user-attachments/assets/1c70022c-3cc5-4450-80de-4fa31f876ff6" />

### Fig.8 Core area

• The internal area of the box is called “Core Area”. 

• The horizontal lines running along the width of Core are “Standard Cell Rows”. Every alternate of them are marked indicating alternate VDD and VSS rows. 

• This setup is called “Flipped Standard Cell Rows”.
<img width="1919" height="1130" alt="Screenshot 2025-11-19 153642" src="https://github.com/user-attachments/assets/e6b4f015-e3a1-425a-a4ca-975d9a075de0" />

### → Floorplan 

#### Steps under Floorplan : 

1. Aspect Ratio [Ratio of Vertical Height to Horizontal Width of Core]

2. Core Utilisation [The total Core Area % to be used for Floor Planning]
 
3. Channel Spacing between Core Boundary to IO Boundary
 
• Select Floorplan → Specify Floorplan to modify/add concerned values to the above Factors. On adding/modifying the concerned values, the core area is also modified.

### Fig.9 Specify Floorplan 

• The Yellow patch on the Left Bottom are the group of “Unassigned pins” which are to be  placed along the IO Boundary along with the Standard Cells [Gates].
<img width="1426" height="860" alt="Screenshot 2025-11-20 082933" src="https://github.com/user-attachments/assets/8ea06195-b50d-4657-ad74-e2614a94e8c8" />

#### → Power Planning

#### Steps under Power Planning : 

1. Connect Global Net Connects
   
2. Adding Power Rings
   
3. Adding Power Strings
   
4. Special Route

Under Connect Global Net Connects, we create two pins, one for VDD and one for VSS connecting them to corresponding Global Nets as mentioned in Globals file / Power and Ground Nets.

1. Select Power → Connect Global Nets.. to create “Pin” and “Connect to Global Net” as shown and use “Add to list”.
   
2. Click on “Apply” to direct the tool in enforcing the Pins and Net connects to Design and then Close the window.
   
• In order to tap in Power from a distant Power supply, Wider Nets and Parallel connections improve efficiency. Moreover, the cells that would be placed inside the core area are expected to have shorter Nets for lower resistance. 

• Hence Power Rings [Around Core Boundary] and Power Stripes [Across Core Boundary] are added which satisfies the above conditions.

• Select Power → Power Planning → Add Rings to add Power rings ‘around Core Boundary’.

• Select the Nets from Browse option OR Directly type in the Global Net Names separated by a space being Case and Spelling Sensitive. 

• Select the Highest Metals marked ‘H’ [Horizontal] for Top and Bottom and Metals marked ‘V’ [Vertical] for Right and Bottom. This is because Highest metals have Highest Widths and thus Lowest Resistance. 

• Click on Update after the selection and “Set Offset : Centre in Channel” in order to get the Minimum Width and Minimum Spacing of the corresponding Metals and then Click “OK”. 

• Similarly, Power Stripes are added using similar content to that of Power Rings.

• On adding Power Stripes, The Power mesh setup is complete as shown. However, There are no Vias that could connect Metal 9 or Metal 8 directly with Metal 1 [VDD or VSS of Standard Cells are generally made up of Metal 1]. 

• The connection between the Highest and Lowest Metals is done through Stacking of Vias done using “Special Route”. 

• To perform Special Route, Select Route → Special Route → Add Nets → OK. 

• After the Special Route is complete, all the Standard Cell Rows turn to the Color coded for Metal 1 

### Fig.10 Power plan 

The complete Power Planning process makes sure Every Standard Cell receives enough power to operate smoothly.
<img width="1918" height="1136" alt="Screenshot 2025-11-19 154641" src="https://github.com/user-attachments/assets/2fe28c87-75a7-48ae-b83c-d98bb6b3871a" />

#### → Placement 

1. The Placement stage deals with Placing of Standard Cells as well as Pins.
    
2. Select Place → Place Standard Cell → Run Full Placement → Mode → Enable ‘Place I/O Pins’ → OK → OK .
   
• All the Standard Cells and Pins are placed as per the communication between them, i.e., Two communicating Cells are placed as close as possible so that shorter Net lengths can be used for connections as Shorter Net Lengths enable Better Timing Results.

### Fig.11 Placement of standard Cells 

• You can toggle the Layer Visibility from the list on the Right. The List of Layers available are shown on the right under “Layer” tab with colour coding.
<img width="1916" height="1128" alt="Screenshot 2025-11-19 161309" src="https://github.com/user-attachments/assets/a986da13-25c5-4da4-a376-43674d17c709" />
<img width="1917" height="1133" alt="Screenshot 2025-11-19 161746" src="https://github.com/user-attachments/assets/b7118f50-f8d0-41d3-9e33-eb8c79ec1a71" />

## Result

Thus, the physical design stages up to placement for the 4-bit up-down counter were completed and verified.
