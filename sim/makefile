DUMP=NONE
LONG=NONE

verdi_path = /usr/synopsys/Verdi3_L-2016.06-1

default :
	echo "\`define  $(DUMP)       "  >    define.v ; 
	echo "\`define  $(LONG)       "  >>   define.v ;
	vcs -full64 -cpp g++-4.8 -cc gcc-4.8  -lca -timescale=1ns/1ps  -P  $(verdi_path)/share/PLI/VCS/LINUX64/novas.tab   $(verdi_path)/share/PLI/VCS/LINUX64/pli.a +vcs+lic+wait +vcd+vcdpluson  -sverilog +verilog2001ext+.v  +lint=TFIPC-L    -debug_all   -f ./tb.vc -top  ahb3lite_sram1rw     -cm line+cond+fsm+tgl -cm_dir ./cov_info      -l vcs_com.log ; 
	./simv       -cm line+cond+fsm+tgl -cm_dir  ./cov_info         -l vcs_sim.log 

verdi:
	verdi -sv  -f ./tb.vc  -top tb_top &

clean:
	rm -rf *simv*  *csrc   *~ verdiLog  novas*  ucli.key  *.vpd  *.fsdb  vc_hdrs.h  *.log      cov_report   cov_info.vdb 
	

cov:
	urg   -full64  -dir     ./*case*/cov_info.vdb    -metric line+cond+fsm+tgl -report   ./cov_report   -format both
	/home/software/firefox/firefox  ./cov_report/hierarchy.html  &

grep:
	grep "CASE"  ./*case*/vcs*.log


gen_v:
	perl my_cat.pl vp.vc   all_vp.sv  vp
	perl my_cat.pl dut.vc  dut.sv v
	perl my_cat.pl lib.vc  lib.sv v
	cat  ../../../example_design/bench/mem/ddr3.sv   >> all.sv
	##vcs -full64 +sv  -protect128 all.sv

emacs:
	cp  ../rtl/cnt.v ./
	emacs   --batch   tx_sys.v           -f verilog-auto     -f save-buffer
	emacs   --batch   tb_top.sv           -f verilog-auto     -f save-buffer



