Tensil
==========================

[![Build status](https://badge.buildkite.com/e44156260ed9775ea72699e45cb394526ea7db24b09c4059aa.svg?branch=master)](https://buildkite.com/tensil/build)

## Tensil toolchain flow

![Flow](/doc/flow.png)

## Setup

1. Download and install [JDK 11 from Azul](https://www.azul.com/downloads/?version=java-11-lts&package=jdk);
2. Download and install [Verilator](https://verilator.org/guide/latest/install.html) (tests only);
3. Clone [Tensil models repo](https://github.com/tensil-ai/tensil_models) on the same level with this repo (tests and demo only);
4. Download and install [Xilinx Vitis or Vivado](https://www.xilinx.com/support/download.html);
5. Download and install [Xilinx PYNQ](http://www.pynq.io/board.html) for your FPGA development platform;
6. Clone [Tensil PYNQ driver](#) to `/home/xilinx` on your FPGA development platform.

## Build command line tools

    $ ./mill '{rtl,tools}.assembly'

## Run full test suite

    $ ./mill __.test -l org.scalatest.tags.Slow -l tensil.tags.Broken

## Compile AI/ML model

Compile AI/ML model (ResNet20 v2 CIFAR) for specific TCU architecture and FPGA development platform ([Avnet Ultra96 v2](https://www.avnet.com/wps/portal/us/products/avnet-boards/avnet-board-families/ultra96-v2/)).

### From frozen TensorFlow graph

    $ ./compile -a ./arch/ultra96v2.tarch -m ../tensil_models/resnet20v2_cifar.pb -o "Identity"

### From ONNX

    $ ./compile -a ./arch/ultra96v2.tarch -m ../tensil_models/resnet20v2_cifar.onnx -o "Identity:0"

## Make Verilog RTL

Make Verilog RTL for specific TCU architecture and FPGA development platform (Ultra96 v2) and 128-bit DRAM AXI.

    $ ./make_rtl -a ./arch/ultra96v2.tarch -d 128

## Create Vivado design

Create Vivado design for specific FPGA development platform (Ultra96 v2).

![Ultra96 v2 design](/doc/ultra96v2_design.png)

## Run AI/ML model on FPGA

Use PYNQ and Jupyter notebooks to run AI/ML model on FPGA.

![Resnet on PYNQ](/doc/resnet20_on_pynq.png)