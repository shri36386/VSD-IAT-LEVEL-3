# VSD-IAT-LEVEL-3

<h2>THEORY</h2>

<details>
  <summary><h2>SKY130 DAY 1 - INCEPTION OF OPEN-SOURCE EDA, OPENLANE AND SKY130 PDK<h2></summary>

 <h3>WHAT IS A PACKAGE</h3>

- PACKAGE IS THE OUTER COVERING, WHICH PROTECTS THE CHIP WITHING ITSELF.
 
- THE CHIP, WHICH CONTAILS THE INSTUCTIONS IS PLACED IN THE MIDDLE OF THE PACKAGE
   
- THE CONNECTIONS FROM THE WIRE TO THE CHIP ARE WIREBOUND.
  
- PACKAGES ARE GIVEN NAMES SUCH AS QFN-48 ETC.

 <h3>WHEN WE OPEN UP A CHIP</h3>

- WHEN WE OPEN UP A CHIP WE FIND VARIOUS DIFFERENT COMPONENTS SUCH AS PADS, DIE AND CORE

- THE PADS HELP IN TRANSFERING INSTRUCTIONS FROM INSIDE THE CHIP TO OUTSIDE THE CHIP. THEY ARE PRESENT IN THE BOUNDRY OF THE CHIP.

- THE CORE CONTAINS THE DIGITAL LOGIC OF THE CHIP.

- BOTH TOGETHER, (CORE AND PADS) MAKE UP THE DIE. THIS IS THE BASIC FUNTIONING UNIT OF SEMICONDUCTOR INDUSTRY.

 <h3>FOUNDRY</h3>

- FOUNDRY IS THE PLACE WHERE THE SEMICONDUCTOR CHIPS ARE MANIFACTURED. 

- IT IS LIKE A FACTORY CONTAING VARIOUS MACHINES TO MAKE CHIPS.

 <h3>RISC-V INSTRUCTION SET ARCHITECTURE</h3>

 - IT CAN BE DESCRIBED AS A LANGUAGE THROUGH WHICH WE CAN COMMUNICATE WITH THE COMPUTER.

 - TO RUN A C-PROGAM ON A PARTICULAR HARDWARE LAYOUT WE NEED TO PASS THIS INFORMATION INTO THE HARDWARE. TO DO THIS THERE IS A PARTICULAR FLOW -

 <h3>FLOW TO PASS INORMATION OF THE C-PROGRAM TO THE HARDWARE LAYOUT</h3>

 - FIRST, THE C-PROGRAM IS COMPILED IN ITS RISC-V ASSEMBLY LANGAUGE PROGRAM.
 
 - THEN IT IS CONVERTED INTO MACHINE LANGUAGE PROGRAM WHICH IS THE BINARY LANGAUGE PROGRAM.

 - AFTER THIS, THE BITS GET EXCECUTED IN THE LAYOUT OF THE HARDWARE.

<h3>APPLICATION POINT OF VIEW  OF THE FLOW</h3>

- THE SOFTWARE WE RUN IN OUR DAY TO DAY LIVES RUNS ON A PARTICULAR HARDWARE PRESENT IN OUR LAPTOPS/CPU'S.

- THE FLOW OF THE INSTRUCTION SET IS AS FOLLOWS

 1. FIRST THE INSTRUCTION SET ENTERS INTO A BOX CALLED SYSTEM SOFTWARE, WHERE THE APPLICATION PROGRAM IS CONVERTED INTO BINARY LANGAUGE. THE COMPONENTS OF THE SYSTEM SOFTWARE ARE OS, COMPILER AND ASSEMBLER.
 
 2. OS - THE OPERATING SYSTEM OR THE OS DOES VARIOUS JOBS SUCH AS HANDLING IO OPERATIONS, ALLOCATES MEMORY, ETC. ASIDE THESE TASKS THE MAIN OPERATION OF THE OS IS TO HELP IN CONVERSION OF THE APPLICATION LANGAUGE TO THE ASSEMBLY LANGAUGE SO THAT IT CAN BE UNDERSTOOD BY THE HARDWARE.
 
 3. COMPILER - THE COMPILER TAKES THE FUNCTION IN C, C++, JAVA LANGAGES AND CONVERTS IT INTO INSTRUCTIONS.
 
 4. ASSEMBLER - THE ASSEMBLER TAKES THERE INSTRUCTIONS ARE CONVERTS THEM INTO THERE RESPECTIVE BINARY INSTRUCTIONS.

<h3>ASIC</h3>

- TO DESIGN A APPLICATION SPECIFIC INGRETED CIRCUIT IN A AUTOMATED WAY THE MAIN COMPONENTS OR TOOLS REQUIRED

1. RTL IP'S - THE DESCRIPTIONS OF THE DIGITAL LOGIC

2. EDA TOOLS - THE SOFTWARE FOR DESIGNING AND SYNTHESIS

3. PDK KITS - CONTAINS FABRICATION RELATED INFORMATION.

<h3>PDK KITS</h3>

- THE PDK OR THE PROCESS DESIGN KIT ACTS AS A INTERFACE BETWEEN THE FABS AND THE DESIGNERS.

- IT CONTAINS VARIOUS TOOLS SUCH AS THE PROCESS DESIGN RULES: DRK, LVS, PEX, DEVICE MODELS, DIGITAL STANDARD CELL LIBRARIES, I/O LIBRARIES ETC.

<h3>SIMPLIFIED RTL TO GDSII FLOW</h3>

- THE SIMPLIFIED FLOW CONSISTS OF THE FOLLOWING STEPS -

- SYNTHESIS -
  1. SYNTHESIS CONVERTS RTL TO A CIRCUIT OUT OF COMPONENTS FROM THE CIRCUIT CELL LIBRARY.
  2. THESE CELLS HAVE REGULAR/STANDARD LAYOUT.

- FLOOR PLANNING AND POWER PLANNING -
  1. HELPS IN PLANNING THE PLACEMENT OF VARIOS PARTS OF A CHIP. IN MACRO FLOOR PLANNING DIMENSIONS, PIN LOCATIONS AND ROWS ARE PLANNED.
  2. IN THE POWER PLANNING THE POWER NETWORK IS CONSTRUCTED. POWER PINS ARE PLACED AND CONNECTED TO METAL STRAPS.

- PLACEMENT -
  1. THE CELLS ARE PLACED ON THE FLOORPLAN ROWS AND ALIGNED WITH THE SITES.
  2. IT IS USUALLY DONE IN 2 STEPS - GLOBAL AND DETAILED.

 - CTS OR CLOCK DISTRIBUTION NETWORK-
   1. IT IS DONE TO DELIVER THE CLOCK TO ALL SEQUENTIAL ELEMENTS
   2. TO DELIVER WITH MINIMUM SKEW AND DELAY (0 IS HARD TO ACHIEVE).

  - ROUTING -
   1. DONE TO INTERCONNECT USING METAL LAYERS.
   2. METAL TRACKS ARE USED TO FORM A ROUTING GRID. ROUTING GRIDS ARE HUGE.
   3. TO EASE THE PROCESS WE CAN DIVIDE AND CONQUER USING THESE TWO APPROACHES.
      A. GLOBAL ROUTING: GENERATES ROUTING GUIDES.
      B. DETAILED ROUTING: USES THESE GUIDES TO IMPLEMENT THE ACTUAL WIRING.

  - SIGN OUT -
  1. IN THIS PROCESS PHYSICAL AND TIMING VERIFICATIONS ARE DONE.
  2. PHYSICAL VERIFICATIONS - dESIGN RULES CHECKING AND LAYOUT VS. SCHEMATIC.
  3. TIMING VERIFICATION - STATIC TIMING ANALYSIS.

  </details>

<details>
  <summary><h2>SKY130 DAY 2 - FLOORPLANS AND INTRODUCTION TO LIBRARY CELLS<h2></summary>

<h3>FLOORPLAN - DEFINE WIDTH AND HEIGHT</h3>

- THE FIRST STEP IN PHYSICAL DESIGNING OVERFLOW, IS TO DETERMINE THE WIDTH AND HEIGHT OF THE CORE AND THE DIE.

- WE BEGIN WITH A NETLIST. A NETLIST DEFINES THE CONNECTIVITY BETWEEN ALL THE COMPONENTS. LET'S CONSIDER A NETLIST WITH 2 FLOPS AND 2 GATES.

- WE ARE FIRST DEPENDENT ON THE SIZE OF THE COMPONENTS, ASSUMING THE LENGHT AND BREDTH OF THESE COMPONENTS ARE 2 UNITS, THE AREA IS 4 SQ. UNITS.

- USING THIS NETLIST AND DIMENSIONS, WE CAN CALCULATE THE AREA OCCPIED ON THE SILICON WAFER. BEFORE DOING SO, WE CAN TRY TO CLUB ALL OF THE COMPONENTS, REMOVING THE WIRES.

- IN THIS CASE, THE LENGHT BECOMES 4 UNITS AND SO DOES THE WIDTH, THE TOTAL AREA COVERED IN 16 SQ. UNITS. BY DOING SO, WE HAVE A ROUGH AREA OCCUPIED OF THE NETLIST.

- WE PLACE OUR LOGIC IN THE CORE WHICH IS ENCAPSULATED BY THE DIE. THE CIRCUIT IS BUILT ON THE CORE.

1. UTILISATION FACTOR = <sup>AREA OCCUPIED BY NETLIST</sup>/<sub>TOTAL AREA OF CORE</sub>

- IN THE ABOVE CASE -  UTILISATION FACTOR = 16/16 = 1. THIS MEANS THE CORE IS COMPLETELY OCCUPIED. WE CANNOT ADD ANY MORE CELLS INTO THE CORE.

- THROUGH THIS CALCUTION WE CAN ENSURE 100% UTILISATION OF THE SILICON WAFER.

- IN A PRACTICAL SCENARIO WE USUALLY GO FOR 50-60% UTILISATION.

2. ASPECT RATIO = <sup>WIDTH</sup>/<sub>HEIGHT</sub>

- IS THE ABOVE CASE - ASPECT RATIO = 4/4 = 1. THIS MEANS THE CHIP IS A SQUARE.

LETS TAKE ANOTHER EXAMPLE -

- LET'S SAY WE HAVE A SQUARE CHIP HAVING LENGTH AND WIDTH OF 8 UNITS AND WE NEED TO PLACE OUR EXISTING CIRCUIT OF 16 SQ. UNITS ON THIS.

- TO CALCULATE THE UTILISATION FACTOR IN THIS CASE IS 16/64 = 0.25

<h3>FLOORPLAN - DEFINE LOCATION OF PREPLACED CELLS</h3>

- PREPLACED CELLS ARE IP'S/ BLOCKS ARE PLACED BEFORE AUTOMATED PLACEMENT AND ROUTING. THEREFORE THEY ARE KNOWN AS PREPLACED CELLS.

- THE ARRANGEMENT OF THESE IP'S ARE REFERRED TO AS FLOOR PLANNING.

- LET'S CONSIDER WE HAVE THREE PREPLACED CELLS BLOCK A, B AND C.

1. IF WE HAVE A DESIGN, WHERE ALL INPUT PINS ARE TO ONE ONE SIDE AND ALL OUPUT PINS ARE TO THE OTHER, AND THE IP'S ARE COMMUNICATING WITH THE INPUT PINS WE TRY TO PLACE THE IP'S TOWARDS THE SIDE WITH THE INPUT PINS.

2. THESE CELLS ARE PLACED IN A PARTICULAR AREA DEPENDING ON THE SCENARIO.

3. AFTER THEY ARE PLACED, THEIR LOCATIONS CAN'Y BE CHANGED. THEREFORE, THEY HAVE TO BE VERY WELL DESIGNED.

<h3>SURROUND THE PREPLACED CELLS WITH DECOUPLING CAPACITORS</h3>

- A DECOUPLING CAPACITOR IS A CAPACITOR USED TO DECOUPLE THE CELLS FROM THE MAIN POWER SUPPLY.

- THE PURPOSE OF DOING SO IS TO DELIVER CURRENT TO THE GATES WHILE SWITCHING.

<h3>POWER SUPPLY</h3>

- IT IS NECESSARY TO HAVE MORE THAN 1 POWER SUPPLY, AR THIS MAY LEAD TO VOLTAGE DROOP IN VDD AND VOLTAGE BUMP IN VSS.

- IF ANY LOGIC IS IN NEED OF POWER, IT ACCQUIRES IT FROM THE NEAREST POWER SUPPLY. THE POWER IS ALSO DROPPED TO THE NEAREST GROUND.

- THIS CONNECTION OF VSS AND VDD IS CALLED AS A MESH.

<h3>PIN PLACEMENT</h3>

- THE CONNECTIVITY BETWEEN THE LOGICS IS CODED USING VERILOG. IT IS CALLED NETLIST.

- TTHE AREA CONSISTING OF INPUTS AND OUTPUTS IS BLOCKED TO ENSURE THAT NO AUTOMATED PLACEMENT IS DONE THERE.

AFTER THE FOLLOWING STEPS, WE ARE DONE WITH FLOOR PLAN AND ARE READY FOR PLACEMENT AND ROUTING.

<h3>PLACEMENT AND ROUTING</h3>

- ALL COMPONENTS, LOGIC GATES, FLIP FLOPS AND IP'S ARE PRESENT IN A SHELF CALLED A LIBRARY.

- ALL THESE COMPONENTS ARE GIVEN A PROPER SHAPE AND SIZE.

- NEXT WE HAVE TO PLACE THE COMPONENETS. WE HAVE A NETLIST AND A FLOORPLAN.

- THE COMPONENETS ARE PLACED BASED ON WHERETHER THEY RECIEVE INPUT OR GIVE OUT THE OUTPUT.

- NEXT WE NEED TO OPTIMIZE PLACEMENT. IN THIS STEP WEESTIMATE WIRE LENGTH AND CAPACITANCE AND BASED ON THAT, WE INSERT REPEATETERS.

- WE CAN ADD BUFERS ACCORDING TO THE REQUIREMENT.

- FROM THE TIME ANALYSIS WE FIGURE OUT WHETHER OUR PLACEMENT IS EFFICIENT.

<h3>CLOCK TREE SYNTHESIS</h3>

- CLOCK TREE SYNTHESIS (CTS) IS USED TO DISTRIBUTE THE CLOCK SIGNAL EVENLY ACROSS ALL SEQUENTIAL ELEMENTS IN A VLSI DESIGN, MINIMIZING SKEW AND INSERTION DELAY.

- IT TAKES PLACEMENT DATA AND CLOCK CONSTRAINTS AS INPUT, THEN INSERTS BUFFERS OR INVERTERS ALONG THE CLOCK ROUTES TO BALANCE DELAYS ACROSS CLOCK INPUTS.

- BEFORE CTS, ALL CLOCK PINS ARE DRIVEN BY A SINGLE SOURCE; AFTER CTS, THE CLOCK TREE IS CONSTRUCTED AND BALANCED TO ENSURE UNIFORM TIMING.

<h3>CELL DESIGN FLOW</h3>

1. STANDARD CELLS

- STANDARD CELLS ENCAPSULATE A SPECIFIC LOGIC FUNCTION SUCH ARE AND GATES, OR GATES, INVERTERS ETC.

- THEY ARE PLACED IN A SECTION KNOWN AS LIBRARY. LIBRARIES HAVE CELLS WITH DIFFERENT FUNCTIONALITY AND SIZE.

2. DESIGN FLOW OF PARTICULAR CELLS

- LET'S TAKE THE EXAMPLE OF AN INVERTER. TO DESIGN IT THERE ARE THREE NECESSARY COMPONENTS

A. INPUTS - PDK KITS: DRC AND LVS RULES, SPICE MODELS, LIBRARY AND USER DEFINED SPACES.

B. DESIGN STEPS - CIRCUIT DESIGN LAYOUT DESIGN AND CHARCTERIZATION.

C. OUTPUTS - CDL.

3. CHARACTERIZATION FLOW STEPS-

- READING SPICE MODULE FILES

- READING NETLIST EXTRACTED BY SPICE
  
- RECOGNIZING BUFFER BEHAVIOR
  
- READING SUBCIRCUITS
  
- SETTING UP THE SIMULATION
  
- ATTACHING NECESSARY POWER SOURCES
  
- APPLYING STIMULUS
  
- FINALIZING THE SIMULATION ENVIRONMENT
  
- PROVIDING NECESSARY OUTPUT CAPACITANCE
  
- PROVISION OF SIMULATION COMMAND

<h3>TIMING CHARACTERIZATION</h3>

1. TIMING THRESHTOLDS -

- THE THRESHOLD VOLTAGE (VTH OR VGS(TH)) IS THE MINIMUM GATE VOLTAGE REQUIRED FOR AN MOSFET TO FORM A CONDUCTIVE CHANNEL BETWEEN SOURCE AND DRAIN, ENABLING CURRENT FLOW.

- SLEW REFERS TO THE TIME OR RATE AT WHICH A SIGNAL TRANSITIONS BETWEEN VOLTAGE LEVELS, ALSO CALLED TRANSITION DELAY.

2. PROPOGATION DELAY -

- PROPAGATION DELAY IS THE TIME FOR A CHANGE IN INPUT TO REFLECT AT THE OUTPUT OF A LOGIC GATE. 

- IN VLSI, IT IS MEASURED AS THE TIME DIFFERENCE BETWEEN THE INPUT AND OUTPUT REACHING 50% OF THEIR FINAL VALUES.

- ALSO CALLED GATE DELAY, IT INDICATES HOW INPUT TRANSITIONS INFLUENCE OUTPUT.

  </details>

<details>
  <summary><h2>SKY130 DAY 3 - DESIGN LIBRARY CELLS<h2></summary>

<h3>SPICE DECK CREATION FOR CMOS INVERTER-</h3>

- IT IS A NETLIST WITH COMPLETE COMPONENT CONECTIVITY.

- THE COMPONENT VALUES ARE TAKEN: FOR THE PMOS, THE DIMENSIONS ARE 0.375µM/0.25µM (WIDTH/LENGTH). IDEALLY, PMOS SHOULD BE 2–3 TIMES WIDER THAN NMOS SINCE HOLE CARRIERS IN PMOS ARE SLOWER THAN ELECTRON CARRIERS IN NMOS. TO MATCH RISE AND FALL TIMES, THE PMOS WIDTH IS INCREASED TO REDUCE RESISTANCE.

- NEXT, WE HAVE TO IDENTIFY AND NAME THE NODES IN THE CIRCUITS.

<h3>STEPS FOR SPICE SIMULATION</h3>

-	OPEN NGSPICE SIMULATOR.

-	LOAD THE CIRCUIT FILE USING THE SOURCE COMMAND.

-	RUN THE SIMULATION WITH THE RUN COMMAND.

-	USE SETPLOT TO CHOOSE AVAILABLE PLOTS.

-	TYPE DISPLAY TO LIST NODES FOR PLOTTING.

-	PLOT THE WAVEFORM USING PLOT OUT VS IN.

<h3>SWITCHING THRESHOLD VM</h3>

- THE GRAPHS' SIMILAR SHAPES INDICATE THAT CMOS IS A ROBUST DEVICE. ITS ROBUSTNESS IS DETERMINED BY SWITCHING THRESHOLD AND PROPAGATION DELAY.
  
- SWITCHING THRESHOLD IS WHERE INPUT VOLTAGE EQUALS OUTPUT VOLTAGE, WITH BOTH PMOS & NMOS IN SATURATION.
  
- AT THIS POINT, LEAKAGE CURRENT INCREASES AS CURRENT FLOWS FROM VDD TO GND, POTENTIALLY CAUSING A SHORT CIRCUIT.

<h3>16 - MASK CMOS PROCESS</h3>

1. SELECTING A SUBSTRATE

- A SUBSTRATE IS SOMETHING ON WHICH WE FABRICATE OUR COMPLETE DESIGN.

- THE MOST FREQUENTLY USED SUBSTRATE IS A P - TYPE, HIGH RESISTIVITY (5, 50 OHMS), DOING LEVEL 10^15 CM^-3, ORIENATATION 100 SUBSTRATE.

- SUBSTRATE DOPING SHOULD BE LESS THAN 'WELL DOPING'.

2. CREATING AN ACTIVE REGION FOR THE TRANSISTORS -

- THE REGIONS ACTUALLY CONTAINING PMOS AND NMOS. WE HAVE TO CREATE A FEW POCKETS ON THE SUBSTRATE.

- THESE POCKETS ARE CALLED ACTIVE REGIONS.

- WE NEED TO CREATE AN ISOLATION BETWEEN THOSE POCKETS BECAUSE THE ACTIVE REGIONS SHOULDN'T INTERFERE WITH EACHOTHER'S WORKING. TO DO SO WE CAN FOLLOW THE BELOW STEPS -

A. GROW A LAYER OF SILICON DIOXIDE WHICH ACTS AS A VERY GOOD INSULATOR. THE THINKNESS IS APPROXIMATELY 40 NANOMETER.

B. NEXT WE HAVE TO DEPOSIT A LAYER OF SILICON NITRATE, THE THINKNESS IS APPROXIMATELY 80 NANOMETER.

C. TO MAKE THE POCKETS, WE NEED TO IDENTIFY THE REGIONS WHERE THE POCKETS WILL BE SITUATED. TO DO THIS WE FIRST DEPOSIT A LAYER OF PHOTORESIST OF 1 MICRON THINKNESS. 

D. ON THIS WE WILL CREATE THE MASK/ LAYOUT 1 WHICH IS LIKE A PROTECTION LAYER. THIS IS CONSTRACTED THROUGH PHOTOLITHOGRAPHY.

E. THE PHOTORESIST STAYS IN THE AREAS WITH THE MASK AND IS ECTCHED OUT FROM THE OTHER AREAS. THEN WE REMOVE THE PHOTORESIST ITSELF.

F. THE CHIP IS PLACED IN FURACE FOR THE OTHER AREAS TO GROW.

G. THE SILICON NITRATE IS REMOVED USING HOT PHOSPHORIC ACID.

3. MAKE P AND N WELLS

A. TO CREATE THE P-WELL AGAIN THE PHOTORESIST IS APLLIED AND ON THIS WE WILL CREATE THE MASK/ LAYOUT 2 WHICH IS LIKE A PROTECTION LAYER.

B. AGAIN THE PHOTORESIST STAYS IN THE AREAS WITH THE MASK AND IS ECTCHED OUT FROM THE OTHER AREAS. 

C. NEXT, BORON IS USED TO MAKE A P-WELL AS IT IS A P-TYPE MATERIAL. THIS CREATES THE P -WELL.

D. TO CREATE THE N-WELL AGAIN THE PHOTORESIST IS APLLIED AND ON THIS WE WILL CREATE THE MASK/ LAYOUT 3 WHICH IS LIKE A PROTECTION LAYER.

E. AGAIN THE PHOTORESIST STAYS IN THE AREAS WITH THE MASK AND IS ECTCHED OUT FROM THE OTHER AREAS. 

F. PHOSPHORUS, IS USED TO MAKE THE N-WELL AS IT IS A N-TYPE MATERIAL. 

G. NEXT THE COMPLETE SUBSET IS TAKEN INTO A HIGH TEMPRATURE FURNACE TO DRIVE IN THE BORON AND PHOSPHORUS TO CREATE PROPER P AND N WELLS.

4. FORMATION OF GATES -

A. WE HAVE TO FABRICATE THE N-MOS TRANSISTOR ON THE P-WELL. TO DO SO, WE APPLY A MASK 4 ON THE N-WELL.

B. BORON IS AGAIN USED AND IT PENETRATES THROUGH THE SILICON OXIDE.

C. WE HAVE TO FABRICATE THE P-MOS TRANSISTOR ON THE N-WELL. TO DO SO, WE APPLY A MASK 4 ON THE P-WELL.

D. ARSENIC IS USED AND IT PENETRATES THROUGH THE SILICON OXIDE.

E. NEXT USING HYDROFLURIC OXIDE WE REMOVE THE SILICON OXIDE LAYER. THEN THE SILICON OXIDE IS AGAIN GROWN.
  
  </details>
