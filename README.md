# pes_fpmul


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
