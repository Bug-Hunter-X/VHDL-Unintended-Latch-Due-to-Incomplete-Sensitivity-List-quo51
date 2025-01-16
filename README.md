# VHDL Unintended Latch Bug

This repository demonstrates a common error in VHDL code: an unintended latch created when a signal in a process isn't included in the sensitivity list.

The bug is demonstrated in `bug.vhdl`. The solution is presented in `bugSolution.vhdl`.

## The Bug

The original code has an incomplete sensitivity list.  The `internal_data` signal is assigned a value within the process but is only sensitive to `clk` and `rst`. This means that any changes to `data_in` outside of the rising edge of the clock will not immediately update `internal_data`. Instead, the previous value of `internal_data` will be retained until the next clock edge, acting as an unintended latch.

## The Solution

The solution adds `data_in` to the sensitivity list of the process. Now, any change in `data_in` will trigger the process, ensuring that `internal_data` is immediately updated, removing the unintended latch.
