# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

 <img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/b5f95c0d-1fd6-4c3c-9a35-11eb9c86cba3" />

#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
```
module alu_32bit_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;	//AND Operation
3'b001:y=a|b;	//OR Operation
3'b010:y=~(a&b);//NAND Operation
3'b011:y=~(a|b);//NOR Operation
3'b100:y=a+b;	//Addition
3'b101:y=a-b;	//Subtraction
3'b110:y=a*b;   //Multiply
3'b111:y=a^b;	// XOR Operation
default:y=32'bx;
endcase 
end 
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_32bit_tb_case; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_32bit_case DUT(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00100001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#150 $finish; 
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using Ifelseif Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;	               //AND Operation 
else if (f==3'b001)
y=a|b;	              //OR Operation
else if (f==3'b010)
y=~(a&b);	      //NAND Operation
else if (f==3'b011)
y=~(a|b);	      //NOR Operation
else if (f==3'b100)
y=~(a^b);	      //XOR Operation
 else if (f==3'b101)
y=a+b;                //Addition
 else if (f==3'b110)
y=a-b;	              //Subtraction 
else if (f==3'b111)
y=a*b;	              //Multiply 
else
y=32'bx; 
end 
endmodule
```

#### Test Bench :
```
module alu_ifelseif_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; b=32'h00100001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#100 $finish; 
endmodule
```

Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below
<img width="1920" height="1080" alt="Screenshot 2025-10-14 101934" src="https://github.com/user-attachments/assets/06a693cb-7866-4a4d-bc9c-af8ebd4b7ec1" />
<img width="1920" height="1080" alt="Screenshot 2025-10-14 112052" src="https://github.com/user-attachments/assets/96aa3b27-6387-4fa4-8216-1005533cbcd5" />

#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
<img width="1920" height="1080" alt="Screenshot 2025-10-14 102147" src="https://github.com/user-attachments/assets/8e22a5c9-8ea9-416f-92e4-121221ed776c" />


#### Fig 3: Nclaunch Window

#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file
<img width="1920" height="1080" alt="Screenshot 2025-10-14 102026" src="https://github.com/user-attachments/assets/b45dd417-3dd5-4735-8b15-0e799c8e89cb" />
<img width="1920" height="1080" alt="Screenshot 2025-10-15 082513" src="https://github.com/user-attachments/assets/49b0c97b-4361-4d5b-aa0f-f425e6221914" />



#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.
<img width="1920" height="1080" alt="Screenshot 2025-10-14 102655" src="https://github.com/user-attachments/assets/743b48cd-e878-4089-8b61-8646944b8321" />
<img width="1920" height="1080" alt="Screenshot 2025-10-15 082944" src="https://github.com/user-attachments/assets/479f27ce-6785-46a8-8f81-f4c9ee13a2d3" />



#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options
<img width="1920" height="1080" alt="Screenshot 2025-10-14 110607" src="https://github.com/user-attachments/assets/57109a60-7a65-4798-ae76-5d78a672c76b" />
<img width="1920" height="1080" alt="Screenshot 2025-10-15 083616" src="https://github.com/user-attachments/assets/d9c9e27a-c20e-4ec4-b424-6255956a1ebc" />


#### Fig 6: Design Browser window for simulation
<img width="1920" height="1080" alt="Screenshot 2025-10-14 110646" src="https://github.com/user-attachments/assets/bdd14921-a287-4e0f-bd31-94dc60330ba4" />
<img width="1920" height="1080" alt="Screenshot 2025-10-15 084114" src="https://github.com/user-attachments/assets/d3eca9f3-7ab8-451a-9935-62785fa16fe8" />



#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.
<img width="1920" height="1080" alt="Screenshot 2025-10-15 084833" src="https://github.com/user-attachments/assets/eb75f96a-29b4-4e87-801d-b0d7787da6f2" />
<img width="1920" height="1080" alt="Screenshot 2025-10-15 084452" src="https://github.com/user-attachments/assets/af87059c-eb58-4ecc-b350-2e2199e94d59" />


#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 094950" src="https://github.com/user-attachments/assets/ac2cdb0c-82b3-4f41-bb71-cfe98a29e223" />
<img width="1920" height="1080" alt="Screenshot 2025-10-14 112254" src="https://github.com/user-attachments/assets/a41e715b-841f-43ae-9228-fc7edd3d2cdd" />


#### Fig 9: Area report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 095022" src="https://github.com/user-attachments/assets/5882de69-2690-4fe0-9364-efac5141b9d8" />
<img width="1920" height="1080" alt="Screenshot 2025-10-14 113203" src="https://github.com/user-attachments/assets/a0bc1cbe-8aae-4d2e-90b5-e9532738f1df" />


#### Fig 10: Power Report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-04 095040" src="https://github.com/user-attachments/assets/7a890f39-e357-4df5-8dcb-d9ddfc9ab499" />
<img width="1920" height="1080" alt="Screenshot 2025-10-14 113216" src="https://github.com/user-attachments/assets/f5cbecc9-f4d5-46f1-b90b-e2ae22b72dd9" />



#### Fig 11: Timing Report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-10-15 085434" src="https://github.com/user-attachments/assets/44bf9298-3aaa-4f91-a73c-d99f8bb41cda" />
<img width="1920" height="1080" alt="Screenshot 2025-10-14 113342" src="https://github.com/user-attachments/assets/39623901-6f0b-42a5-9b97-6d84a23dc6b3" />


#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct
<img width="464" height="292" alt="image" src="https://github.com/user-attachments/assets/53908eca-8736-4eb9-88c8-d6b40c86f465" />


## Result
The 32-bit ALU designs implemented using behavioural case statements and if–elseif constructs were successfully verified using the Incisive simulation environment (ncvlog/ncsim) for all applied test vectors. Both RTL descriptions were found to be functionally correct, synthesizable, and capable of producing identical outputs across all operations. Cadence Genus synthesis generated corresponding gate-level netlists and produced detailed reports for area and power.

Based on the synthesis observations, the if–elseif–based ALU demonstrates better efficiency, achieving a lower total cell area (9913.876 µm²) compared to the case-based ALU (10254.481 µm²). Power results also indicate that the if–elseif model consumes slightly lower total logic, leakage, internal, and switching power. Although both designs meet functional requirements, the if–elseif architecture shows marginal improvements in area and power, while the case-based design is comparatively larger and consumes marginally more power.
