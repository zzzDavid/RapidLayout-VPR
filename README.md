# RapidLayout-VPR

## Introduction

In the paper *RapidLayout: Fast Hard Block Placement for FPGA-optimized Systolic Arrays using Evolutionary Algorithms*, we compare evolutionary placement algorithms with VPR's annealer. This repo provides a complete guide of setting up the VPR experiment.

## Set up VPR

First, clone the repo on a Linux machine:

```
$ git clone https://github.com/zzzDavid/RapidLayout-VPR.git
$ cd RapidLayout-VPR/vpr
```

The vpr binary is already compiled. To run the placement experiments under the same settings, we defined an architecture file `my_arch.xml` and a netlist file `conv.blif`.

`my_arch.xml` reproduces the columnar hard block distribution of Xilinx VU11P device. It defines a resource region equivalent to half of a SLR of the VU11P FPGA. 

`conv.blif` tries to capture the hard block connections of the original systolic array design. It defines a netlist containing 80 convolution units, which will be mapped to the resource region.

To run the placement design once with GUI, execute:

```
$  ./vpr my_arch.xml conv.blif -place
```
After the netlist and architecture file are parsed, it outputs the resource report:

```
The circuit will be mapped into a 200 x 96 array of clbs.

Resource usage...
	Netlist      0	blocks of type: <EMPTY>
	Architecture 4	blocks of type: <EMPTY>
	Netlist      962	blocks of type: io
	Architecture 4736	blocks of type: io
	Netlist      0	blocks of type: clb
	Architecture 14400	blocks of type: clb
	Netlist      1440	blocks of type: dsp
	Architecture 1488	blocks of type: dsp
	Netlist      640	blocks of type: block_ram
	Architecture 672	blocks of type: block_ram
	Netlist      160	blocks of type: ultra_ram
	Architecture 160	blocks of type: ultra_ram
```
And the GUI displays the initial placement:

<div align="center">
  <img width="90%" height="50%"
  src="https://res.cloudinary.com/dxzx2bxch/image/upload/v1592905476/Screen_Shot_2020-06-23_at_17.34.37_hufvuv.png">
</div>

Then, click "Proceed", the tool will run the placement experiment and output the results as `conv.place` file:

<div align="center">
    <img width=70% height="50%"
    src="https://res.cloudinary.com/dxzx2bxch/image/upload/v1592905475/Screen_Shot_2020-06-23_at_17.36.58_evcd0s.png">
</div>    


**Produce the results in the paper**:

In the RapidLayout repository, we provide tools to automatically run VPR without GUI and translate the results back for evaluation. Please refer to RapidLayout's documentation for details.

## License

This tool is distributed under MIT license.

Copyright (c) 2020 Niansong Zhang, Nachiket Kapre

<div style="text-align: justify;">
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
<br><br>
</div>


<div style="text-align: justify;">
<b>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.</b>
<br><br>
</div>


<div style="text-align: justify;">
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
 </div>