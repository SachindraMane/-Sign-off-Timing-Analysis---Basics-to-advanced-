## Sign-off Timing Analysis - Basics to advanced


![staimage](https://user-images.githubusercontent.com/47828728/220837107-5eb5cdf2-9ebc-4cd1-9eb4-e782d8d7ef79.jpg)

# OpenSTA is a gate level static timing verifier. As a stand-alone executable it can be used to verify the timing of a design using standard file formats like :-

-> Verilog netlist

-> Liberty library

-> SDC timing constraints

-> SDF delay annotation

-> SPEF parasitics

OpenSTA is architected to be easily bolted on to other tools as a timing engine.
By using a network adapter, OpenSTAcan access the host netlist data structures without duplicating them.
Query based incremental update of delays, arrival and required times & Simulator to propagate constants from constraints and netlist tie high/low

Reference for commands used in OpenSTA :

https://github.com/Bharti-Navlani/VSD-IAT-Sign-off-Timing-Analysis_Basics-to-Advance/files/10786440/OpenSTA.pdf

## Table Of Content:-

1) Lab_1

2) Lab_2

3) Lab_3

4) Lab_4

5) Lab_5

# Lab_1 (Day_1):-

Inputs to OpenSTA :-

Verilog Model : Contains the Standard Cells

![Screenshot (200)](https://user-images.githubusercontent.com/47828728/220838055-908e3ee2-acc1-4892-8ca6-4b179f312a6c.png)

Liberty File
    
                 leafpad sky130_fd_sc_hd_tt_025C_1v80.lib
                 
 ![Screenshot (226)](https://user-images.githubusercontent.com/47828728/220838421-de318475-a150-40b3-b04e-f2e45d2e6e70.png)
 
 Instantiated nand2 cell and  INPUT/OUTPUT pins of nand2 cell
 
 ![Screenshot (201)](https://user-images.githubusercontent.com/47828728/220838671-d3025aac-ae2c-48b3-bdad-b19437c5fd8d.png)
 
 ![Screenshot (202)](https://user-images.githubusercontent.com/47828728/220838731-a0aac50c-f653-4158-b2f5-055b2f48629c.png)
 
![Screenshot (203)](https://user-images.githubusercontent.com/47828728/220838739-d5db82d9-795b-49c3-aad2-7da22a4f0435.png)

![Screenshot (204)](https://user-images.githubusercontent.com/47828728/220838741-8c602fc3-d25a-4992-9b2d-1729923c0ad8.png)

Clock

                  create_clock –period 50 –name tau2015_clk [get_ports tau2015_clk]
                  
 ![Screenshot (228)](https://user-images.githubusercontent.com/47828728/220838936-59406693-887e-42b5-995d-3eaf059058f4.png)
 
 Run Script
 
 In runscript we define all the commands we want to run in the openSTA tool.
 
                  leafpad run.tcl

![Screenshot (208)](https://user-images.githubusercontent.com/47828728/220839227-63f870e5-da88-4f49-8a75-60ce97b3c2f6.png)


Run OpenSTA

               sta run.tcl -exit | tee run.log

![Screenshot (230)](https://user-images.githubusercontent.com/47828728/220839430-f3131107-be47-4f44-8343-f20ed5c8d447.png)


Reports the Timing results:


![Screenshot (210)](https://user-images.githubusercontent.com/47828728/220840009-a0b544fc-da37-4219-ace6-24d5d3ece255.png)

![Screenshot (211)](https://user-images.githubusercontent.com/47828728/220840018-241ebdc6-62aa-4d3e-a078-efe276c34c91.png)


## Lab_2 (Day_2):-

### Exercise_1:-

### Q1)  Find all the cells in simple_max.lib.

 Command Used		
    
    
				      grep -c "Begin cell" simple_max.lib"
              
List of the cells present in the simple_max.lib

 
![cell](https://user-images.githubusercontent.com/47828728/220842521-196ed38f-006c-4df1-9dc5-07af4113483b.png)


### Q2)  Find all the pins of the cell NAND2_X1 in simple_max.lib
   
   
           input pins : pin("a") and pin("b")
           output pin : pin("o")
   
   
![Screenshot (235)](https://user-images.githubusercontent.com/47828728/220844350-bb8d30f3-2616-4c77-a0cd-48d1146afbe5.png)

![Screenshot (236)](https://user-images.githubusercontent.com/47828728/220844357-fb5b66e3-c092-40b8-ac17-ac59032fd8bb.png)


### Q3)  What difference you see between NAND2_X1 and NAND3_X1


![Screenshot (237)](https://user-images.githubusercontent.com/47828728/220847729-92d22015-aa0d-48e9-9475-d008808cdee0.png)


### Q4) What is the difference between ‘simple_max.lib’ and ‘simple_min.lib’
 
On comparing simple_max.lib and simple_min.lib file it is observed that parameter like delay, fall_transition , cell_rise , rise_transition, cell_fall etc is different in both the files. In simple_max.lib file maximum value is defined for all the parameters while in simple_min.lib minimum value is defined.


### Exercise_2:-

Other paths in run.log :-

![Screenshot (241)](https://user-images.githubusercontent.com/47828728/220850350-59bc239a-0401-4bca-99e5-6c813dfbfee6.png)



 
# Lab_3 (Day_3):-

## Running the lab:-
 Command used:-
 
		sta run.tcl -noexit | tee out.txt


![Screenshot (242)](https://user-images.githubusercontent.com/47828728/220870802-1427c408-c07e-4885-a85e-c6446ea7698a.png)



out.txt file:-

		                     leafpad out.txt
				     
![image](https://user-images.githubusercontent.com/47828728/220877941-d216ae9c-0312-4927-9219-fe8196b9f90c.png)

				     
### Slack calculation:-
 
Understanding the slack computation ->

Path for which the slack is -217.323 is shown below circuit daigram ->

![Screenshot (245)](https://user-images.githubusercontent.com/47828728/220875353-cb3d732f-bccf-4ca6-994c-baab8c9da1b6.png)

## Exercise :-

Change the number of paths:-

![image](https://user-images.githubusercontent.com/47828728/220877629-9bd93fa6-3115-47e0-aae6-83626b47cf7e.png)

![123](https://user-images.githubusercontent.com/47828728/220883755-944612e0-a304-4054-908d-3979ade5ffe5.png)


### Path_1 
           
	    F1:CK -> U6 -> U4 -> U5:A1 -> U7:A2 -> F2:D
	    
![Screenshot (247)](https://user-images.githubusercontent.com/47828728/220882798-f98efa92-13f5-42e4-9575-a8a89e0c0bc3.png)


### Path_2

	   F1:CK -> U3 -> U4 -> U6:A2 -> U7:A1 -> F2:D
	   
![Screenshot (248)](https://user-images.githubusercontent.com/47828728/220882854-7c455111-24f4-482b-8634-7095c7d9e567.png)


### Path_3

	   F1:CK-> U3 -> U5:A1 -> U7:A2 -> F2:D

![Screenshot (249)](https://user-images.githubusercontent.com/47828728/220882982-ed95eef9-dfac-470f-a91f-8d2d4af6fa86.png)



### Path_4

	  F1:CK -> U6:A1 -> U7:A1 -> F2:D
	  
![Screenshot (250)](https://user-images.githubusercontent.com/47828728/220883031-1ad7612a-a351-431d-90df-67a4c41b3c6c.png)

	  
### Path_5

	  F1:CK -> U3 -> U5:A2 -> U7:A2 -> F2:D
	  
![Screenshot (251)](https://user-images.githubusercontent.com/47828728/220883200-fe88d8bb-5d81-4acb-96d0-e1ebab5c521e.png)

	  
### Path_6

	  F1:CK -> U3 -> U4 -> U6:A2 -> U7:A1 -> F2:D
	  
![Screenshot (252)](https://user-images.githubusercontent.com/47828728/220883238-d6ec8457-2c36-47ef-8b16-0d6e0fa19584.png)

	  
### Path_7

	F1:CK -> U6 -> U4 -> U5:A1 -> U7:A2 -> F2:D
	
![Screenshot (253)](https://user-images.githubusercontent.com/47828728/220883282-fd446223-c93c-4e13-9ce0-d234f146f3ae.png)

	
### Path_8

	F1:CK -> U6:A1 -> U7:A1 -> F2:D
	

![Screenshot (254)](https://user-images.githubusercontent.com/47828728/220883322-a6799793-0354-49eb-b70c-0ff0028a3779.png)
	

## Lab_4 (Day_4):-

### Clock Gating Checks

Gating techniques used is ‘Active Low Clock Gating'

			cd lab6
	                leafpad run.tcl

![image](https://user-images.githubusercontent.com/47828728/220886478-dba3803b-c8c6-4eeb-ba46-a0ee9439d866.png)

		      
		        sta run.tcl –exit | tee run.log


### SLACK ON CLOCK GATING PATH REPORTED

![Screenshot (256)](https://user-images.githubusercontent.com/47828728/220886943-2ea27d0b-bf7e-49ae-8e16-61c7d1b92e4b.png)
![Screenshot (257)](https://user-images.githubusercontent.com/47828728/220887127-f4aa310c-cae4-488f-96af-af0cd57d2dc4.png)

### Async Pin Checks
 			
			cd lab7					 
			leafpad run.tcl

![image](https://user-images.githubusercontent.com/47828728/220887366-6c15644e-caa8-4e0e-a632-05dd8a513b8b.png)

		      sta run.tcl –exit | tee run.log

![Screenshot (259)](https://user-images.githubusercontent.com/47828728/220887602-c98e6719-d4d7-4acc-9a0b-3da6cbe798d7.png)


# Lab_5 (Day_5):-

Common Path Pessimism Removal(CPPR) Common path pessimism removal (CPPR) is the removal of artificially-induced pessimism between a launch and capture flip-flop pair during timing analysis by identifying the common clock path between launch and capture clock paths.

![image](https://user-images.githubusercontent.com/47828728/220888622-45ada244-39ff-4036-a79c-91805c888571.png)

### Timing report before CPPR :-

			cd lab4
			sta run.tcl –exit | tee out.txt


