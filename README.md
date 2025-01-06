# Chip Design but Open Source
## Open Template
- From [Tiny Tapeout Verilog Template](https://github.com/TinyTapeout/tt10-verilog-template), convert it into a template to your account
- `src/project.v` is the verilog file to be used.
- Modify the verilog file to
  ```verilog
  `default_nettype none
  module tt_um_example (
      input  wire [1:0] ui_in,    // Dedicated inputs
      output wire [1:0] uo_out,   // Dedicated outputs
  );
  
    // All output pins must be assigned. If not used, assign to 0.
      assign uo_out[0] = ui_in[1] ^ ui_in[0];  //sum
      assign uo_out[1] = ui_in[1] & ui_in[0]; //carry
  
  endmodule
  ```
