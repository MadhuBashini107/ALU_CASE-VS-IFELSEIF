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
```verilog
module alu_32(input [31:0]a,
input [31:0]b,
input [2:0]op,
output reg [31:0]res);
always@(*)
begin
	case(op)
		3'b000: res = a+b;
		3'b001: res = a-b;
		3'b010: res = a&b;
		3'b011: res = a|b;
		3'b100: res = ~(a&b);
		3'b101: res = ~(a|b);
		3'b110: res = a^b;
		3'b111: res = a<<1;
		default: res = 32'd0;
	endcase
end
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```verilog
module alu_32_tb;
reg [31:0]a;
reg [31:0]b;
reg [2:0]op;
wire [31:0]res;
alu_32 uut (a,b,op,res);
initial
begin
	a = 32'd10;#10;
	b = 32'd5;#10;
	op = 3'b000;#10;
	op = 3'b001;#10;
	op = 3'b010;#10;
	op = 3'b011;#10;
	op = 3'b100;#10;
	op = 3'b101;#10;
	op = 3'b110;#10;
	op = 3'b111;#10;
	$finish;
end
endmodule	
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using If Statement :
```verilog
module alu_32(input[31:0]a,
input [31:0]b,
input [2:0]op,
output reg [31:0]res);
always @ (*)
begin
	if(op == 3'b000)
		res = a+b;
	else if (op == 3'b001)
		res = a-b;
	else if (op == 3'b010)
		res = a&b;
	else if (op == 3'b011)
		res = a|b;
	else if (op == 3'b100)
		res = a^b;
	else if (op == 3'b101)
		res = ~(a&b);
	else if (op == 3'b110)
		res = ~(a|b);
	else if (op == 3'b111)
		res = a<<1;
	else
		res = 32'b0;
end
endmodule
```

#### Test Bench :
```verilog
module alu_32_tb;
reg [31:0]a;
reg [31:0]b;
reg [2:0]op;
wire [31:0]res;

alu_32 uut(a,b,op,res);
initial
begin
	a = 32'd10;
	b = 32'd5;
	op = 3'b000;#10;
	op = 3'b001;#10;
	op = 3'b010;#10;
	op = 3'b011;#10;
	op = 3'b100;#10;
	op = 3'b101;#10;
	op = 3'b110;#10;
	op = 3'b111;#10;
	$finish;
end
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
<img width="1209" height="484" alt="image" src="https://github.com/user-attachments/assets/21583848-b1bd-4c38-8dbf-a06d701947b0" />


#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.

#### Fig 3: Nclaunch Window
<img width="1918" height="1077" alt="image" src="https://github.com/user-attachments/assets/2f8a3f85-4eea-4951-9fdd-3dc1f95fe877" />


#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/a1f7b34e-9d35-44f1-8958-991be76ecf22" />

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

#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

<img width="1916" height="1077" alt="image" src="https://github.com/user-attachments/assets/b1d71de9-57bb-478b-850e-84f1565f2a3f" />

#### Fig 6: Design Browser window for simulation
ALU Case:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f6bfdc69-6fb3-48e3-911e-425ca1481c35" />

ALU If-Else:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/63dec625-cffd-4809-9fd4-7843842608c9" />

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

#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
ALU Case:

<img width="1919" height="1074" alt="image" src="https://github.com/user-attachments/assets/9202e655-17d3-4cce-8747-e1923cade90d" />

ALU If-Else:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f6771b69-f736-4a91-9953-87e39b3382e6" />


#### Fig 9: Area report of case and ifelseif construct
ALU Case:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/3794fe6b-2bb2-4349-812a-34afc8cc6b4b" />

ALU If-Else:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f614a6a4-b9a4-4bc1-9cf2-54209c13fd20" />


#### Fig 10: Power Report of case and ifelseif construct
ALU Case:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/7aee7296-5332-4218-ae3f-5e6a542ea9a6" />

ALU If-Else:

<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/e95e881b-66cc-47c3-8027-2abda3d41bbd" />


#### Fig 11: Timing Report of case and ifelseif construct

ALU Case:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/3dfdc8b6-5755-48e7-8efd-551fdb100e7d" />

ALU If-Else:

<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/dc961a5d-2a86-4b6c-9f0f-9ba372cbf1cc" />


#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

<img width="1397" height="88" alt="image" src="https://github.com/user-attachments/assets/267c525a-85e9-4eb8-b5bc-0dfb8e54773e" />


## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors. Both implementations were functionally correct and synthesizable. Synthesis using Cadence Genus generated gate-level netlists along with area, timing, and power reports.
A comparative analysis revealed that the case-statement-based ALU resulted in slightly lower area and better timing performance, while the if–elseif-based ALU exhibited higher logic complexity and marginally increased delay due to sequential decision evaluation. Both designs, however, produced identical functional outputs.
