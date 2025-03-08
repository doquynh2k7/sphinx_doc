.. _gettingstarted:

===============
Getting Started
===============

Join the Corundum community
===========================

To stay up to date with the latest developments and get support, consider joining the `mailing list <https://groups.google.com/d/forum/corundum-nic>`_ and `Zulip <https://corundum.zulipchat.com/>`_.

Obtaining the source code
=========================

The main `upstream repository for Corundum <https://github.com/corundum/corundum/>`_ is located on `GitHub <https://github.com/>`_.  There are two main ways to download the source code - downloading an archive, or cloning with git.  

To clone via HTTPS, run::

    $ git clone https://github.com/corundum/corundum.git

To clone via SSH, run::

    $ git clone git@github.com:corundum/corundum.git

Alternatively, download a zip file::

    $ wget https://github.com/corundum/corundum/archive/refs/heads/master.zip
    $ unzip master.zip

Or a gzipped tar archive file::

    $ wget https://github.com/corundum/corundum/archive/refs/heads/master.tar.gz
    $ tar xvf master.tar.gz

There is also a `mirror of the repository <https://gitee.com/alexforencich/corundum/>`_ on `gitee <https://gitee.com/>`_, here are the equivalent commands::

    $ git clone https://gitee.com/alexforencich/corundum.git
    $ git clone git@gitee.com:alexforencich/corundum.git
    $ wget https://gitee.com/alexforencich/corundum/repository/archive/master.zip
    $ wget https://gitee.com/alexforencich/corundum/repository/archive/master.tar.gz

Setting up the FPGA development environment
===========================================

Corundum currently uses `Icarus Verilog <http://iverilog.icarus.com/>`_ and `cocotb <https://github.com/cocotb/cocotb>`_ for simulation.  Linux is the recommended operating system for a development environment due to the use of symlinks (which can cause problems on Windows as they are not supported by windows filesystems), however WSL may also work well.

The required system packages are:

* Python 3 (``python`` or ``python3``, depending on distribution)
* Icarus Verilog (``iverilog``)
* GTKWave (``gtkwave``)

The required python packages are:

* ``cocotb``
* ``cocotb-bus``
* ``cocotb-test``
* ``cocotbext-axi``
* ``cocotbext-eth``
* ``cocotbext-pcie``
* ``pytest``
* ``scapy``

Recommended additional python packages:

* ``tox`` (to run pytest inside a python virtual environment)
* ``pytest-xdist`` (to run tests in parallel with `pytest -n auto`)
* ``pytest-sugar`` (makes pytest output a bit nicer)

It is recommended to install the required system packages via the system package manager (``apt``, ``yum``, ``pacman``, etc.) and then install the required Python packages as user packages via ``pip`` (or ``pip3``, depending on distribution).

Running tests
=============

Once the packages are installed, you should be able to run the tests.  There are several ways to do this.

First, all tests can be run by runing ``tox`` in the repo root.  In this case, tox will set up a python virtual environment and install all python dependencies inside the virtual environment.  Additionally, tox will run pytest as ``pytest -n auto`` so it will run tests in parallel on multiple CPUs. ::

    $ cd /path/to/corundum/
    $ tox
    py3 create: /home/alex/Projects/corundum/.tox/py3
    py3 installdeps: pytest == 6.2.5, pytest-xdist == 2.4.0, pytest-split == 0.4.0, cocotb == 1.6.1, cocotb-test == 0.2.1, cocotbext-axi == 0.1.18, cocotbext-eth == 0.1.18, cocotbext-pcie == 0.1.20, scapy == 2.4.5
    py3 installed: attrs==21.4.0,cocotb==1.6.1,cocotb-bus==0.2.1,cocotb-test==0.2.1,cocotbext-axi==0.1.18,cocotbext-eth==0.1.18,cocotbext-pcie==0.1.20,execnet==1.9.0,iniconfig==1.1.1,packaging==21.3,pluggy==1.0.0,py==1.11.0,pyparsing==3.0.7,pytest==6.2.5,pytest-forked==1.4.0,pytest-split==0.4.0,pytest-xdist==2.4.0,scapy==2.4.5,toml==0.10.2
    py3 run-test-pre: PYTHONHASHSEED='4023917175'
    py3 run-test: commands[0] | pytest -n auto
    ============================= test session starts ==============================
    platform linux -- Python 3.9.7, pytest-6.2.5, py-1.11.0, pluggy-1.0.0
    cachedir: .tox/py3/.pytest_cache
    rootdir: /home/alex/Projects/corundum, configfile: tox.ini, testpaths: fpga, fpga/app
    plugins: forked-1.4.0, split-0.4.0, cocotb-test-0.2.1, xdist-2.4.0
    gw0 [69] / gw1 [69] / gw2 [69] / gw3 [69] / gw4 [69] / gw5 [69] / gw6 [69] / gw7 [69] / gw8 [69] / gw9 [69] / gw10 [69] / gw11 [69] / gw12 [69] / gw13 [69] / gw14 [69] / gw15 [69] / gw16 [69] / gw17 [69] / gw18 [69] / gw19 [69] / gw20 [69] / gw21 [69] / gw22 [69] / gw23 [69] / gw24 [69] / gw25 [69] / gw26 [69] / gw27 [69] / gw28 [69] / gw29 [69] / gw30 [69] / gw31 [69] / gw32 [69] / gw33 [69] / gw34 [69] / gw35 [69] / gw36 [69] / gw37 [69] / gw38 [69] / gw39 [69] / gw40 [69] / gw41 [69] / gw42 [69] / gw43 [69] / gw44 [69] / gw45 [69] / gw46 [69] / gw47 [69] / gw48 [69] / gw49 [69] / gw50 [69] / gw51 [69] / gw52 [69] / gw53 [69] / gw54 [69] / gw55 [69] / gw56 [69] / gw57 [69] / gw58 [69] / gw59 [69] / gw60 [69] / gw61 [69] / gw62 [69] / gw63 [69]
    .....................................................................    [100%]
    ======================= 69 passed in 1534.87s (0:25:34) ========================
    ___________________________________ summary ____________________________________
      py3: commands succeeded
      congratulations :)

Second, all tests can be run by running ``pytest`` in the repo root.  Running as ``pytest -n auto`` is recommended to run multiple tests in parallel on multiple CPUs. ::

    $ cd /path/to/corundum/
    $ pytest -n auto
    ============================= test session starts ==============================
    platform linux -- Python 3.9.7, pytest-6.2.5, py-1.10.0, pluggy-0.13.1
    rootdir: /home/alex/Projects/corundum, configfile: tox.ini, testpaths: fpga, fpga/app
    plugins: split-0.3.0, parallel-0.1.0, cocotb-test-0.2.0, forked-1.3.0, metadata-1.11.0, xdist-2.4.0, html-3.1.1, cov-2.12.1, flake8-1.0.7
    gw0 [69] / gw1 [69] / gw2 [69] / gw3 [69] / gw4 [69] / gw5 [69] / gw6 [69] / gw7 [69] / gw8 [69] / gw9 [69] / gw10 [69] / gw11 [69] / gw12 [69] / gw13 [69] / gw14 [69] / gw15 [69] / gw16 [69] / gw17 [69] / gw18 [69] / gw19 [69] / gw20 [69] / gw21 [69] / gw22 [69] / gw23 [69] / gw24 [69] / gw25 [69] / gw26 [69] / gw27 [69] / gw28 [69] / gw29 [69] / gw30 [69] / gw31 [69] / gw32 [69] / gw33 [69] / gw34 [69] / gw35 [69] / gw36 [69] / gw37 [69] / gw38 [69] / gw39 [69] / gw40 [69] / gw41 [69] / gw42 [69] / gw43 [69] / gw44 [69] / gw45 [69] / gw46 [69] / gw47 [69] / gw48 [69] / gw49 [69] / gw50 [69] / gw51 [69] / gw52 [69] / gw53 [69] / gw54 [69] / gw55 [69] / gw56 [69] / gw57 [69] / gw58 [69] / gw59 [69] / gw60 [69] / gw61 [69] / gw62 [69] / gw63 [69]
    .....................................................................    [100%]
    ======================= 69 passed in in 2032.42s (0:33:52) =====================

Third, groups of tests can be run by running ``pytest`` in a subdirectory.  Running as ``pytest -n auto`` is recommended to run multiple tests in parallel on multiple CPUs. ::

    $ cd /path/to/corundum/fpga/common/tb/rx_hash
    $ pytest -n 4
    ============================= test session starts ==============================
    platform linux -- Python 3.9.7, pytest-6.2.5, py-1.10.0, pluggy-0.13.1
    rootdir: /home/alex/Projects/corundum, configfile: tox.ini
    plugins: split-0.3.0, parallel-0.1.0, cocotb-test-0.2.0, forked-1.3.0, metadata-1.11.0, xdist-2.4.0, html-3.1.1, cov-2.12.1, flake8-1.0.7
    gw0 [2] / gw1 [2] / gw2 [2] / gw3 [2]
    ..                                                                       [100%]
    ============================== 2 passed in 37.49s ==============================

Finally, individual tests can be run by runing ``make``.  This method provides the capability of overriding parameters and enabling waveform dumps in FST format that are viewable in gtkwave. ::

    $ cd /path/to/corundum/fpga/common/tb/rx_hash
    $ make WAVES=1
    make -f Makefile results.xml
    make[1]: Entering directory '/home/alex/Projects/corundum/fpga/common/tb/rx_hash'
    echo 'module iverilog_dump();' > iverilog_dump.v
    echo 'initial begin' >> iverilog_dump.v
    echo '    $dumpfile("rx_hash.fst");' >> iverilog_dump.v
    echo '    $dumpvars(0, rx_hash);' >> iverilog_dump.v
    echo 'end' >> iverilog_dump.v
    echo 'endmodule' >> iverilog_dump.v
    /usr/bin/iverilog -o sim_build/sim.vvp -D COCOTB_SIM=1 -s rx_hash -P rx_hash.DATA_WIDTH=64 -P rx_hash.KEEP_WIDTH=8 -s iverilog_dump -f sim_build/cmds.f -g2012   ../../rtl/rx_hash.v iverilog_dump.v
    MODULE=test_rx_hash TESTCASE= TOPLEVEL=rx_hash TOPLEVEL_LANG=verilog \
             /usr/bin/vvp -M /home/alex/.local/lib/python3.9/site-packages/cocotb/libs -m libcocotbvpi_icarus   sim_build/sim.vvp -fst
         -.--ns INFO     cocotb.gpi                         ..mbed/gpi_embed.cpp:76   in set_program_name_in_venv        Did not detect Python virtual environment. Using system-wide Python interpreter
         -.--ns INFO     cocotb.gpi                         ../gpi/GpiCommon.cpp:99   in gpi_print_registered_impl       VPI registered
         0.00ns INFO     Running on Icarus Verilog version 11.0 (stable)
         0.00ns INFO     Running tests with cocotb v1.7.0.dev0 from /home/alex/.local/lib/python3.9/site-packages/cocotb
         0.00ns INFO     Seeding Python random module with 1643529566
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     Found test test_rx_hash.run_test
         0.00ns INFO     running run_test (1/8)
         0.00ns INFO     AXI stream source
         0.00ns INFO     cocotbext-axi version 0.1.19
         0.00ns INFO     Copyright (c) 2020 Alex Forencich
         0.00ns INFO     https://github.com/alexforencich/cocotbext-axi
         0.00ns INFO     AXI stream source configuration:
         0.00ns INFO       Byte size: 8 bits
         0.00ns INFO       Data width: 64 bits (8 bytes)
         0.00ns INFO     AXI stream source signals:
         0.00ns INFO       tdata width: 64 bits
         0.00ns INFO       tdest: not present
         0.00ns INFO       tid: not present
         0.00ns INFO       tkeep width: 8 bits
         0.00ns INFO       tlast width: 1 bits
         0.00ns INFO       tready: not present
         0.00ns INFO       tuser: not present
         0.00ns INFO       tvalid width: 1 bits
         0.00ns INFO     Reset de-asserted
         0.00ns INFO     Reset de-asserted
    FST info: dumpfile rx_hash.fst opened for output.
         4.00ns INFO     Reset asserted
         4.00ns INFO     Reset asserted
        12.00ns INFO     Reset de-asserted
        12.00ns INFO     Reset de-asserted
        20.00ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x90\x00\x00'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=20000, sim_time_end=None)
        28.00ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x90\x00\x00\x01'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=28000, sim_time_end=None)
        36.00ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x90\x00\x00\x01\x02'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=36000, sim_time_end=None)
        40.00ns INFO     RX hash: 0x00000000 (expected: 0x00000000) type: HashType.0 (expected: HashType.0)
        48.00ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x90\x00\x00\x01\x02\x03'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=48000, sim_time_end=None)
        48.00ns INFO     RX hash: 0x00000000 (expected: 0x00000000) type: HashType.0 (expected: HashType.0)
        56.00ns INFO     RX hash: 0x00000000 (expected: 0x00000000) type: HashType.0 (expected: HashType.0)


    ################    skip a very large number of lines    ################


    252652.01ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x08\x00E\x00\x00V\x00\x8b\x00\x00@\x06d\xff\n\x01\x00\x8b\n\x02\x00\x8b\x00\x8b\x10\x8b\x00\x00\x00\x00\x00\x00\x00\x00P\x02 \x00ms\x00\x00\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=252652007, sim_time_end=None)
    252744.01ns INFO     RX hash: 0xa2a55ee3 (expected: 0xa2a55ee3) type: HashType.TCP|IPV4 (expected: HashType.TCP|IPV4)
    252860.01ns INFO     TX frame: AxiStreamFrame(tdata=bytearray(b'\xda\xd1\xd2\xd3\xd4\xd5ZQRSTU\x08\x00E\x00\x00V\x00\x8c\x00\x00@\x06d\xfc\n\x01\x00\x8c\n\x02\x00\x8c\x00\x8c\x10\x8c\x00\x00\x00\x00\x00\x00\x00\x00P\x02 \x00mo\x00\x00\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-'), tkeep=None, tid=None, tdest=None, tuser=None, sim_time_start=252860007, sim_time_end=None)
    252952.01ns INFO     RX hash: 0x6308c813 (expected: 0x6308c813) type: HashType.TCP|IPV4 (expected: HashType.TCP|IPV4)
    252960.01ns INFO     run_test passed
    252960.01ns INFO     **************************************************************************************
                         ** TEST                          STATUS  SIM TIME (ns)  REAL TIME (s)  RATIO (ns/s) **
                         **************************************************************************************
                         ** test_rx_hash.run_test          PASS       11144.00           1.14       9781.95  **
                         ** test_rx_hash.run_test          PASS       44448.00           3.80      11688.88  **
                         ** test_rx_hash.run_test          PASS       12532.00           1.40       8943.27  **
                         ** test_rx_hash.run_test          PASS       49984.00           4.42      11302.44  **
                         ** test_rx_hash.run_test          PASS       13088.00           1.54       8479.38  **
                         ** test_rx_hash.run_test          PASS       52208.00           4.62      11308.18  **
                         ** test_rx_hash.run_test          PASS       13940.00           1.65       8461.27  **
                         ** test_rx_hash.run_test          PASS       55616.00           5.03      11046.45  **
                         **************************************************************************************
                         ** TESTS=8 PASS=8 FAIL=0 SKIP=0             252960.01          25.11      10073.76  **
                         **************************************************************************************
                         
    make[1]: Leaving directory '/home/alex/Projects/corundum/fpga/common/tb/rx_hash'

Setting up the FPGA build environment (Vivado)
==============================================

Building FPGA configurations for Xilinx devices requires `Vivado <https://www.xilinx.com/products/design-tools/vivado.html>`_.  Linux is the recommended operating system for a build environment due to the use of symlinks (which can cause problems on Windows) and makefiles for build automation.  Additionally, Vivado uses more CPU cores for building on Linux than on Windows.  It is not recommended to run Vivado inside of a virtual machine as Vivado uses a significant amount of RAM during the build process.  Download and install the appropriate version of Vivado.  Make sure to install device support for your target device; support for other devices can be disabled to save disk space.

Licenses may be required, depending on the target device.  A bare install of Vivado without any licenses runs in "WebPACK" mode and has limited device support.  If your target device is on the `WebPACK device list <https://www.xilinx.com/products/design-tools/vivado/vivado-webpack.html#architecture>`_, then no Vivado license is required.  Otherwise, you will need access to a Vivado license to build the design.

Additionally, the 100G MAC IP cores on UltraScale and UltraScale+ require separate licenses.  These licenses are free of charge, and can be generated for `UltraScale <https://www.xilinx.com/products/intellectual-property/cmac.html>`_ and `UltraScale+ <https://www.xilinx.com/products/intellectual-property/cmac_usplus.html>`_.  If your target design uses the 100G CMAC IP, then you will need one of these licenses to build the design.

For example: if you want to build a 100G design for an Alveo U50, you will not need a Vivado license as the U50 is supported under WebPACK, but you will need to generate a (free-of-charge) license for the CMAC IP for UltraScale+.

Before building a design with Vivado, you'll have to source the appropriate settings file.  For example::

    $ source /opt/Xilinx/Vivado/2020.2/settings64.sh
    $ make

Building the FPGA configuration
===============================

Each design contains a set of makefiles for automating the build process.  To use the makefile, simply source the settings file for the required toolchain and then run ``make``.  Note that the repository makes significant use of symbolic links, so it is highly recommended to build the design under Linux.

For example::

    $ cd /path/to/corundum/fpga/mqnic/[board]/fpga_[variant]/fpga
    $ source /opt/Xilinx/Vivado/2020.2/settings64.sh
    $ make

Building the driver
===================

To build the driver, you will first need to install the required compiler and kernel source code packages.  After these packages are installed, simply run ``make``. ::

    $ cd /path/to/corundum/modules/mqnic
    $ make

Note that the driver currently does not support RHEL, centos, and related distributions that use very old and significantly modified kernels where the reported kernel version number is not a reliable indication of the internal kernel API.

Building the userspace tools
============================

To build the userspace tools, you will first need to install the required compiler packages.  After these packages are installed, simply run ``make``. ::

    $ cd /path/to/corundum/utils
    $ make

Setting up the PetaLinux build environment
==========================================

Building PetaLinux projects for Xilinx devices requires `PetaLinux Tools <https://www.xilinx.com/products/design-tools/embedded-software/petalinux-sdk.html>`_.  Linux is the recommended operating system for a build environment due to the use of symlinks (which can cause problems on Windows) and makefiles for build automation.  Download and install the appropriate version of PetaLinux Tools.  Make sure to install device support for your target device; support for other devices can be disabled to save disk space.

An example for a PetaLinux project in Corundum is accompanying the FPGA design using the Xilinx ZynqMP SoC as host system for mqnic on the Xilinx ZCU106 board.  See `fpga/mqnic/ZCU106/fpga_zynqmp/README.md`.

Before building a PetaLinux project, you'll have to source the appropriate settings file.  For example::

    $ source /opt/Xilinx/PetaLinux/2021.1/settings.sh
    $ make -C path/to/petalinux/project build-boot

