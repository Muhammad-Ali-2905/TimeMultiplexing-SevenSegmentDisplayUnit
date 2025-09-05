# Time Multiplexing Seven Segment Display Unit

- Time multiplexing a seven-segment display unit (SSDU) on the **Nexys 3** can drive multiple displays with limited pins. Since the board has limited outputs, you can’t connect each segment of all four displays directly. **Time-division multiplexing (TDM)** rapidly switches which digit is shown on the same set of segments so the hardware is shared across all four displays. This reduces required pins versus wiring each segment individually and makes the design more cost-effective—important for resource-constrained systems.

- The Nexys 3 uses a **100 MHz** crystal oscillator, whose clock period is **10⁻⁸ s**. The FPGA pin connected to the oscillator is **V10**; connect this pin to the **`clk`** input of your module.

- To multiplex each SSDU, refresh it within **1–4 ms**. If we choose **4 ms** per SSDU, the Verilog counter must count up to  
  `4 × 10⁻³ / 10⁻⁸ = 400,000` cycles.  
  Therefore the counter needs `ceil(log2(400000))` bits. Use a small **digit counter** (0–3) to track which SSDU’s data is currently being displayed on the seven-segment unit.
