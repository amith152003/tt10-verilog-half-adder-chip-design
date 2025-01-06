# Half Adder IC Design Documentation

## How it Works

This project implements a **Half Adder** in Verilog, designed to perform a simple addition operation on two 1-bit binary inputs. The core function of the half adder is to compute two outputs:
- **Sum (S)**: The result of the XOR operation on the two input bits.
- **Carry (C)**: The result of the AND operation on the two input bits.

The module is designed to be part of an integrated circuit (IC), and it uses dedicated and IO pins for input, output, and control. The design also handles reset and clock signals.

## How to Test

To test the Half Adder, you can provide various combinations of 1-bit inputs (A and B) and observe the corresponding outputs. The testing steps are as follows:

1. **Input Values**: Set the values for the two input signals, `ui_in[1]` (A) and `ui_in[0]` (B), which represent the two 1-bit binary inputs.
   - A = 0, B = 0
   - A = 0, B = 1
   - A = 1, B = 0
   - A = 1, B = 1

2. **Outputs**: The sum and carry outputs will be available at `uo_out[0]` (sum) and `uo_out[1]` (carry) respectively. You can observe these values using a testbench or directly from the pin outputs.

3. **Reset**: Apply a low signal (`rst_n = 0`) to reset the module before starting the test to ensure the outputs are initialized.

4. **Clock and Enable**: The design includes a clock (`clk`) and enable (`ena`) input, though these are not actively used in this simple design but can be added for simulation purposes.

## External Hardware

This project does not require any complex external hardware but can be tested on an FPGA or ASIC design board. The inputs and outputs are mapped to the following pins:

- **ui_in**: 8-bit wide input, but only the first 2 bits are used for the Half Adder (A and B). The rest are tied to 0.
- **uo_out**: 8-bit wide output, but only the first 2 bits are used for the sum and carry.
- **uio_in/uio_out**: These are IOs for handling input/output operations, but they are unused in the actual operation of the half adder, and are set to 0.
- **uio_oe**: Output enable signal, set to 0, indicating that the outputs are not actively driven in this design.
- **ena**: Active high, but unused in the simple design.
- **clk**: A clock signal, but not needed for this combinational logic.
- **rst_n**: Active low reset to initialize the design.

