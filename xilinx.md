# Xilinx Resources

- [What's `implementation` in Xilinx?](https://www.xilinx.com/support/documentation/sw_manuals/xilinx11/ise_c_implement_fpga_design.htm)
    - Logic Optimization
    - Technology Mapping
    - Place and Route
- [Using Tcl Scripting v2018](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2018_2/ug894-vivado-tcl-scripting.pdf)
- [What is `.xdc`?](https://github.com/Digilent/digilent-xdc/)
	- [Using Constraints v2017](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_4/ug903-vivado-using-constraints.pdf)

- `How to connect IPs?` I came to this question when I tried to build blocks in HLS and Verilog, and was thinking about how should I connect those blocks? There are so many clk, reset, valid signal combinations, is there a standard for this communication protocol? Indeed, there are. This thread collects information about this topic.
	- [Some basic knowledge](http://que.no/index.php/2016/03/13/principles-of-fpga-ip-interconnect/)
	- [Introduction to AXI Protocol: Understanding the AXI interface](https://community.arm.com/soc/b/blog/posts/introduction-to-axi-protocol-understanding-the-axi-interface)
	- [Xilinx AXI4, AXI-Lite, AXI-Stream Homepage](https://www.xilinx.com/products/intellectual-property/axi.html#details)
	- AMBA® 4 AXI4-Stream Protocol
		- The AXI4-Stream protocol requires that all transfers remain __ordered__. It does not permit the reordering of transfers.
		- __AXI4-Stream removes the requirement for an address phase altogether and allows unlimited data burst size. AXI4-Stream interfaces and transfers do not have address phases and are therefore not considered to be memory-mapped.__
	- Summary:
		- AXI4 has many channels, each channel has its own TVALID,
		TREADY and more. AXI-Lite is a subset of AXI4. AXI-stream is more
		simpilifed, in the sense that it actually only has one channel, which
		means only one TVALID, TREADY signals. AXI-stream is unidirectional
		between master and slave.
		- Like the tri-mode MAC, it is using AXI-stream for both TX and
		RX path. That means, if I want to build a new IP block to talk
		with MAC, my new IP only needs to conform with AXI-stream
		protocol.
	- `UG1037: AXI Reference`.
	- `PG035: AXI4-Stream Interconnect`.
	- `PG085 AXI4-Stream Infrastructure IP Suite`.


- [I/O and Clock Planning](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_3/ug899-vivado-io-clock-planning.pdf)

- IP
	- [Ethernet](https://www.xilinx.com/products/technology/ethernet.html)
		- [Tri-Mode Ethernet MAC](https://www.xilinx.com/products/intellectual-property/temac.html)
		- [AXI 1G/2.5G Ethernet](https://www.xilinx.com/products/intellectual-property/axi_ethernet.html#documentation)
		- [AXI Ethernet LITE](https://www.xilinx.com/products/intellectual-property/axi_ethernetlite.html)
		- [10G MAC](https://www.xilinx.com/products/intellectual-property/do-di-10gemac.html#documentation)
	- [Clock Wizard](https://www.xilinx.com/products/intellectual-property/clocking_wizard.html#documentation)

- HLS
  	- `Data I/O protocols`: those are directives that control how the input/output signals interact with outside users.
    	- ap_hs
    	- ap_vld
		- ap_ack
	- `Block-level I/O protocols`: this allows the RTL design to be controlled by additional ports independently of the data I/O ports.
    	- ap_ctrl_hs
    	- ap_ctrl_none
    	- ap_ctrl_chained
    	- s_axilite
    	- which one should I use?