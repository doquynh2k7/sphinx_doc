.. _mod_mqnic_core:

==============
``mqnic_core``
==============

``mqnic_core`` is the core integration-level module for mqnic for all host interfaces.  Contains the interfaces, asynchronous FIFOs, PTP subsystem, statistics collection subsystem, and application block.

For maximum flexibility, this module does not contain the actual host-facing DMA engine, so a wrapper is required to provide the DMA engine with the proper host-facing interface.  The available wrappers are:

* :ref:`mod_mqnic_core_pcie` for PCI express
* :ref:`mod_mqnic_core_axi` for AXI
