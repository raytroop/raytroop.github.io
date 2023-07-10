---
title: verilog readmemb and readmemh
date: 2022-02-12 17:15:47
tags:
categories:
- digital
---

**`$readmemh("hex_memory_file.mem", memory_array, [start_address], [end_address])`**
**`$readmemb("bin_memory_file.mem", memory_array, [start_address], [end_address])`**

The system task has no versions to accept octal data or decimal data.

- The 1st argument is the data file name.
- The 2nd argument is the array to receive the data.
- The 3rd argument is an optional start address, and if you provide it, you can also provide
- The 4th argument optional end address.

Note, the 3rd and 4th argument address is for array not data file.

If the memory addresses are not specified anywhere, then the system tasks load file data sequentially  from the lowest address toward the highest address. 

> The standard before 2005 specify that the system tasks load file data sequentially
> from the left memory address bound to the right memory address bound.

**readtest.v**

```verilog
module readfile;
	reg [7:0] array4 [0:3];
	reg [7:0] array7 [6:0];
	reg [7:0] array12 [11:0];

	integer i;

	initial begin
		$readmemb("data.txt", array4);
		$readmemb("data.txt", array7, 2, 5);
		$readmemb("data.txt", array12);

		for (i = 0; i < 4; i = i+1)
			$display("array4[%0d] = %b", i, array4[i]);

		$display("=========================");

		for (i = 0; i < 7; i = i+1)
			$display("array7[%0d] = %b", i, array7[i]);

		$display("=========================");

		for (i = 0; i < 12; i = i+1)
			$display("array12[%0d] = %b", i, array12[i]);
	end
endmodule
```
**data.txt**

```
00000000 
00000001
00000010
00000011
00000100
00000101
00000110
00001000
```
**result**

```
array4[0] = 00000000
array4[1] = 00000001
array4[2] = 00000010
array4[3] = 00000011
=========================
array7[0] = xxxxxxxx
array7[1] = xxxxxxxx
array7[2] = 00000000
array7[3] = 00000001
array7[4] = 00000010
array7[5] = 00000011
array7[6] = xxxxxxxx
=========================
array12[0] = 00000000
array12[1] = 00000001
array12[2] = 00000010
array12[3] = 00000011
array12[4] = 00000100
array12[5] = 00000101
array12[6] = 00000110
array12[7] = 00001000
array12[8] = xxxxxxxx
array12[9] = xxxxxxxx
array12[10] = xxxxxxxx
array12[11] = xxxxxxxx
```

---

**ref**

[Initialize Memory in Verilog](https://projectf.io/posts/initialize-memory-in-verilog/)
