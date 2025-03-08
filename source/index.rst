.. _intro:

============
Introduction
============


This is a normal text paragraph. The next paragraph is a code sample::

   It is not processed in any way, except
   that the indentation is removed.

   It can span multiple lines.

This is a normal text paragraph again.


Rhodonite is a high-performance :term:`ROCE`-based :term:`RNIC` and platform for High Performance Computer (HPC).

Features include a high performance datapath, 10G/100G Ethernet, PCI express gen 3, a custom, high performance, tightly-integrated :term:`PCIe` :term:`DMA` engine, many (1000+) transmit, receive, completion, and event queues, scatter/gather DMA, :term:`MSI`, multiple interfaces, multiple ports per interface, per-port transmit scheduling including high precision TDMA, flow hashing, :term:`RSS`, checksum offloading, and native IEEE 1588 :term:`PTP` timestamping.  A Linux driver is included that integrates with the Linux networking stack.  Development and debugging is facilitated by an extensive simulation framework that covers the entire system from a simulation model of the driver and PCI express interface on one side to the Ethernet interfaces on the other side.

Rhodonite also provides an application section for implementing custom logic.  The application section has a dedicated PCIe BAR for control and a number of interfaces that provide access to the core datapath and DMA infrastructure.

Rhodonite currently supports devices from both Xilinx and Intel, on boards from several different manufacturers.  Designs are included for the following FPGA boards; see device_list for more details:

*  Xilinx Alveo U250 (Xilinx Virtex UltraScale+ XCU250)
*  Xilinx KU5P (Xilinx Virtex UltraScale+ XCKU5P)




.. only:: html

    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`
