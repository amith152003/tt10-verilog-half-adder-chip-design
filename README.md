# Chip Design but Open Source
## Open Template
- From [Tiny Tapeout Verilog Template](https://github.com/TinyTapeout/tt10-verilog-template), convert it into a template to your account
- `src/project.v` is the verilog file to be used.
- Modify the verilog file to
  ```verilog
  `default_nettype none

  module tt_um_halfadder (
      input  wire [7:0] ui_in,    // Dedicated inputs
      output wire [7:0] uo_out,   // Dedicated outputs
      input  wire [7:0] uio_in,   // IOs: Input path
      output wire [7:0] uio_out,  // IOs: Output path
      output wire [7:0] uio_oe,   // IOs: Enable path (active high: 0=input, 1=output)
      input  wire       ena,      // always 1 when the design is powered, so you can ignore it
      input  wire       clk,      // clock
      input  wire       rst_n     // reset_n - low to reset
  );
  
  
    // All used pins.
      assign uo_out[0] = ui_in[1] ^ ui_in[0];  //sum
      assign uo_out[1] = ui_in[1] & ui_in[0]; //carry

    // All unused pins to be assigned to ground or 0.
      assign uio_out = 0;
      assign uio_oe  = 0;
      assign uo_out[7:2] = 6'b0;

    // List all unused inputs to prevent warnings
      wire _unused = &{ena, clk, rst_n, 1'b0};

  endmodule
  ```
- Open the `src/config.json` to check for any `CLOCK_PERIOD` errors.
- Open the `info.yaml` and change the information as required
  ``` to_change
  #1.
  title:        "Half Adder"      # Project title
  author:       "amith152003"      # Your name
  discord:      ""      # Your discord username, for communication and automatically assigning you a Tapeout role (optional)
  description:  "Open Source Chip Half Adder Design"      # One line description of what your project does
  language:     "Verilog" # other examples include SystemVerilog, Amaranth, VHDL, etc
  clock_hz:     0       # Clock frequency in Hz (or 0 if not applicable)

  #2.
  # Your top module name must start with "tt_um_". Make it unique by including your github username:
  top_module:  "tt_um_halfadder"

  #3.
  # The pinout of your project. Leave unused pins blank. DO NOT delete or add any pins.
  pinout:
    # Inputs
    ui[0]: "a"
    ui[1]: "b"

  #4.
    # Outputs
    uo[0]: "sum"
    uo[1]: "carryout"
  ```
- Open and edit `docs/info.md` for the datasheet.
- Open and modify `test/tb.v`
  ``` verilog
   31| tt_um_halfadder user_project 
  ```
- Open `docs/test.py` and comment the lines using `#` after line 25.
- Go to the repository settings
- Go to Pages
- Change the source from `Deploy from branch` to `Github Actions`
- Go to Actions ->
- Go to `docs` -> `Run workflow` List -> Click on `Run workflow`
- After an eternity the workflow would be completed. (If an error occurs, there would be a problem in the test code)
- Go to `gds` -> `Run workflow` List -> Click on `Run workflow`
- Go to `test` -> `Run workflow` List -> Click on `Run workflow`
- Click on the completed GDS job and scroll down to `view summary` -> Click on `Load summary`
- View the 2D or 3D Viewer for visualizing the design.
