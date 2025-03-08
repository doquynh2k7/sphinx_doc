.. _modules_overview:

========
Overview
========

Corundum has several unique architectural features.  First, hardware queue states are stored efficiently in FPGA block RAM, enabling support for thousands of individually-controllable queues.  These queues are associated with interfaces, and each interface can have multiple ports, each with its own independent transmit scheduler.  This enables extremely fine-grained control over packet transmission.  The scheduler module is designed to be modified or swapped out completely to implement different transmit scheduling schemes, including experimental schedulers.  Coupled with PTP time synchronization, this enables time-based scheduling, including high precision TDMA.

The design of Corundum is  modular and highly parametrized.  Many configuration and structural options can be set at synthesis time by Verilog parameters, including interface and port counts, queue counts, memory sizes, etc.  These design parameters are exposed in configuration registers that the driver reads to determine the NIC configuration, enabling the same driver to support many different boards and configurations without modification.

High-level overview
===================

.. _fig_overview_block:
.. figure:: /diagrams/svg/corundum_block.svg

    Block diagram of the Corundum NIC. PCIe HIP: PCIe hard IP core; AXIL M: AXI lite master; DMA IF: DMA interface; AXI M: AXI master; PHC: PTP hardware clock; TXQ: transmit queue manager; TXCQ: transmit completion queue manager; RXQ: receive queue manager; RXCQ: receive completion queue manager; EQ: event queue manager; MAC + PHY: Ethernet media access controller (MAC) and physical interface layer (PHY).

A  block diagram of the Corundum NIC is shown in :numref:`fig_overview_block`.  At a high level, the NIC consists of several hierarchy levels.  The top-level module primarily contains support and interfacing components. These components include the PCI express hard IP core and Ethernet interface components including MACs, PHYs, and associated serializers, along with an instance of an appropriate :ref:`mod_mqnic_core` wrapper, which provides the DMA interface.