# Aim: 

Write a verilog code for 32 bit ALU supporting four logical and four arithmetic operations,use case statement and if statement for ALU behavioral modeling.

To Verify the Functionality using Test Bench.

# Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

## Design Information and Bock Diagram:

The ALU will take in two 32-bit values, and control line. An Arithmetic unit does the following task like addition subtraction, multiplication and logical operations. As the input is given in 32 bit we get 32 bit output. The arithmetic will show only one output at a time so a selector is necessary to select one of the operator.

![image](https://github.com/user-attachments/assets/e574788c-253f-46da-8468-298fe2844f7a)

### Fig 1 : Block Diagram of 32 Bit ALU 

## Creating a Work space :

Create a folder in your name (Note: Give folder name without any space) and Create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

## Creating Source Codes 

In the Terminal, type gedit <filename>.v (ex: gedit alu_32bit.v). 

A Blank Document opens up into which the following source code can be typed down. 

(Note : File name should be with HDL Extension)

## a)To Verify the Functionality using Test Bench

## Source Code – Using Case Statement :



Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Creating Test bench:
```
module alu_32bit_case(y, a, b, f);
  input [31:0] a;
  input [31:0] b;
  input [2:0] f;
  output reg [31:0] y;

  always @(*) begin
    case(f)
      3'b000: y = a & b;       // AND
      3'b001: y = a | b;       // OR
      3'b010: y = ~(a & b);    // NAND
      3'b011: y = ~(a | b);    // NOR
      3'b100: y = a + b;       // ADD
      3'b101: y = a - b;       // SUB
      3'b110: y = a * b;       // MUL
      default: y = 32'bx;      // Undefined
    endcase
  end

endmodule
```

Similarly, create your test bench using gedit <filename_tb>.v or <filename_tb>.vhdl to open a new blank document (alu_32bit_tb_case).

## Test Bench :

```
module test_alu_32bit_case;

  reg [31:0] a;
  reg [31:0] b;
  reg [2:0] f;
  wire [31:0] y;

  // Instantiate the ALU module
  alu_32bit_case uut (
    .y(y),
    .a(a),
    .b(b),
    .f(f)
  );

  initial begin
    // Test AND
    a = 32'hAAAAAAAA; b = 32'h55555555; f = 3'b000; #10;
    
    // Test OR
    a = 32'hAAAAAAAA; b = 32'h55555555; f = 3'b001; #10;

    // Test NAND
    a = 32'hFFFFFFFF; b = 32'h00000000; f = 3'b010; #10;

    // Test NOR
    a = 32'h00000000; b = 32'h00000000; f = 3'b011; #10;

    // Test ADD
    a = 32'd100; b = 32'd25; f = 3'b100; #10;

    // Test SUB
    a = 32'd100; b = 32'd25; f = 3'b101; #10;

    // Test MUL
    a = 32'd10; b = 32'd3; f = 3'b110; #10;

    // Test default
    f = 3'b111; #10;

    $finish;
  end

endmodule
```

Use Save option or Ctrl+S to save the code or click on the save option from the top most right corner and close the text file.

## Functional Simulation: 

Invoke the cadence environment by type the below commands 

tcsh (Invokes C-Shell) 

source /cadence/install/cshrc (mention the path of the tools) 

(The path of cshrc could vary depending on the installation destination)
      
After this you can see the window like below 

### Fig 2: Invoke the Cadence Environment
![Screenshot 2025-04-28 151800](https://github.com/user-attachments/assets/94ece4b1-dc05-4dd9-98c6-d6c286d3abea)

To Launch Simulation tool 

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design 

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG 


It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .

### Fig 3: Setting Multi-step simulation
![Screenshot 2025-04-28 151819](https://github.com/user-attachments/assets/c2cfd90f-b4eb-4ea2-9d7d-eeded953e5be)


Select Multiple Step and then select “Create cds.lib File” as shown in below figure 

Click the cds.lib file and save the file by clicking on Save option 

### Fig 4:cds.lib file Creation
![Screenshot 2025-04-28 151819](https://github.com/user-attachments/assets/8aac2005-b0ed-4023-a3ef-a9b508c23ffc)

Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. 

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .

We are simulating verilog design without using any libraries 

A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure 



### Fig 5: Selection of Don’t include any libraries
![Screenshot 2025-04-28 151835](https://github.com/user-attachments/assets/6e815cec-d3c6-4540-aaa9-d61568822c62)

A ‘NCLaunch window’ appears as shown in figure below

Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .

To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. 

### Fig 6: Nclaunch Window
![Screenshot 2025-04-28 151907](https://github.com/user-attachments/assets/88ed9a1a-d4a4-4847-8442-b86709539758)

## Step 1: Compilation:

– Process to check the correct Verilog language syntax and usage 

Inputs: Supplied are Verilog design and test bench codes 

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file 

## 	Steps for compilation: 

1. Create work/library directory (most of the latest simulation tools creates automatically)
   
2. Map the work to library created (most of the latest simulation tools creates automatically)
   
3. Run the compile command with compile options
   
i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v 

Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation 

### Fig 7: Compiled database in worklib
![Screenshot 2025-04-28 151950](https://github.com/user-attachments/assets/fcf8e2cb-57e7-4e74-a8f5-dd579e6acbcf)

After compilation it will come under worklib you can see in right side window

Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. 

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical

directory paths. For this Design, you will define a library called “worklib”

#3 Step 2: Elaboration:– 

To check the port connections in hierarchical design

Inputs: Top level design / test bench Verilog codes 

Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file 

## 	Steps for elaboration 

– Run the elaboration command with elaborate options 

1.It builds the module hierarchy

2.Binds modules to module instances 

3.Computes parameter values

4.Checks for hierarchical names conflicts

5.It also establishes net connectivity and prepares all of this for simulation

After elaboration the file will come under snapshot. Select the test bench and simulate it.

## Fig 8: Elaboration Launch Option
![Screenshot 2025-04-28 152222](https://github.com/user-attachments/assets/95034c4b-c19e-47df-a6a1-0abd3538964b)

## Step 3: Simulation: 

– Simulate with the given test vectors over a period of time to observe the output behaviour. 

Inputs: Compiled and Elaborated top level module name 

Outputs: Simulation log file, waveforms for debugging 

Simulation allow to dump design and test bench signals into a waveform 

Steps for simulation – Run the simulation command with simulator options

## Fig 9: Design Browser window for simulation
![Screenshot 2025-04-28 152245](https://github.com/user-attachments/assets/d040bb39-3eaf-4a68-ae2d-2f2c231cbb13)

## Fig 10:Simulation Waveform Window
![Screenshot 2025-04-28 152338](https://github.com/user-attachments/assets/b5843554-fd4f-4736-a396-afa816750a75)

## Fig 11:Simulation Waveform Window
![Screenshot 2025-04-28 152350](https://github.com/user-attachments/assets/4d869cc7-fcdc-4b43-915c-cc45b079e5d2)

### Result

The functionality of a 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool.














      







