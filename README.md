# pes_fpmul
## Floating point Multiplication
### IEEE-754 32-bit Single-Precision Floating-Point Numbers
In 32-bit single-precision floating-point representation:

- The most significant bit is the sign bit (S), with 0 for positive numbers and 1 for negative numbers.
- The following 8 bits represent exponent (E).
- The remaining 23 bits represents fraction (F) also called as Mantessa.
- These FP number have a bias value of 127.
![image](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/0aa72463-7f14-4e95-bcbd-b3407da466a7)

In this project, simplified FP numbers of 11 bits are used consisting of:
- Sign -> 1 bit
- Exponent -> 6 bits
- Mantessa -> 4 bits
- Bias -> 31
## Multiplication of Floating point number
1. **XOR the sign bits:**
  Take the sign bits of the two floating-point numbers and perform an XOR operation. This determines the sign of the resulting product.
2. **Denormalize the exponents:**
  Subtract the bias (a constant value specific to the floating-point representation) from each exponent. This step adjusts the exponents to a denormalized form.
3. **Add the exponents:**
  Add the denormalized exponents together. This sum represents the combined exponent of the resulting product.
4. **Add 1 as MSB for the mantissa and multiply the same:**
 Adjust the mantissas of the two floating-point numbers. Specifically, add 1 as the most significant bit (MSB) of each mantissa. This step prepares the mantissas for multiplication.
5. **Check and adjust the exponent:**
  After multiplying the adjusted mantissas, check the MSB (most significant bit) of the resulting product. If the MSB is 1 (indicating a normalized result), add the bias back to the exponent sum obtained in step 
  This adjustment ensures the exponent correctly reflects the normalization of the product.
   


## Simulation
```bash=
iverilog fpmul.v fpmul_tb.v
./a.out
gtkwave output.vcd
```
![sim_cmd](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/b6ae81cb-906a-4991-9afa-d66ef33ee7f9)


### Output:
![simulation](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/bf8d12e1-fe0e-46da-b139-dca7a85561db)


## Synthesis:
### commands:
```bash=
yosys
read_liberty -lib <liberty file>
read_verilog <design file>
synth -top pes_fpmul
abc -liberty <liberty file>
show
write_verilog control_netlist.v
```
## Schematic:

![schematic](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/10fb8ec7-d7eb-4ed4-984e-c7a45eedf06d)

## Gate level simulation
### Commands:
```bash=
iverilog <primitive.v file ><verilog of the library used for synthesis><designfile><test_bench>
./a.out
gtkwave output.vcd
```
### Output:

![GLS](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/923cc53e-1ade-4e03-a2cc-00fa63d51e90)

# Openlane Flow
* Set up your design file by using the following command:
  
   ``` prep -design <design_file>```

![prep_design](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/5f63fcc7-108e-44b6-b287-62c691564224)


## Synthesis
Command: ```run_synthesis```

![run_synth](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/0e0a2d67-6d16-48b8-ab92-801943a9a3a7)

Report:

![synth_1](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/3cec6b16-d601-44e4-b7ac-13f78c9a3d6b)

![synth_2](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/bbb9c7e7-c58f-41dd-8fba-b14ee26bdec4)

## Floorplan
Command: ```run_floorplan```

![run_flr](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/9486a949-bdfb-4ccd-8f31-4ed567cf58a2)


To view design:

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read merged.nom.lef def pes_fpmul.def```

![floorplan](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/47c9ba18-18d5-40ba-8840-cde4c0b2c045)

![floorplan_zoomed](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/18521c59-9f1b-4678-9b7b-b5f8c907df60)





## Placement
Command: ```run_placement```

![run_place](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/bec4dae0-99e2-477e-83c2-655111a920bd)

To view design:

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read merged.nom.lef def pes_fpmul.def```


![placement](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/2eda2374-7199-408e-ae5c-0c0e3ed4cb4c)

![placement_zoomed](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/5beb01d9-d829-42c5-893b-ebb8e678fff3)





## Clock tree Synthesis(CTS)
Command: ```run_cts```

![run_cts](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/94bec581-1394-4d90-9b73-d9882eb4949a)

To view design:

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read merged.nom.lef def pes_fpmul_cts.def```


![cts](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/343d1ce0-ca8c-4d04-8386-cefbb7c2ba86)

![cts_zoomed](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/2e26ddc4-a12a-4933-887e-c5f0774266bd)


## Routing
Command: ```run_routing```

![run_rout](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/9f3a7b30-a33e-4f25-9086-6cd94715f737)


To view design:
```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read merged.nom.lef def pes_fpmul_rout.def```

![rounting](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/1efe4c5f-a15e-4b98-b90a-b30f211bb2fa)


![rounting_zoomed](https://github.com/GauthamMulay/pes_fpmul/assets/113660503/b93184a8-1bda-4bea-a7b1-709b2a397e90)




