
# PES_ASIC_Class



## Installation of the riscv tool

 -> Install by running these commands in terminal.

```bash
  git clone https://github.com/kunalg123/riscv_workshop_collaterals
cd riscv_workshop_collaterals
chmod 755 run.sh
./run.sh 
```

## CourseWork

### Week 1

<details>
  <summary> Week 1 : Day 1 - Introduction to RISCV ISA and GNU Compiler Toolchain </summary>
  <br>



## C program That calculates sum from 1 to N
____Compiling it using C compiler____
```
gcc sum1ton.c 
./a.out
```





____Compiling using RISCV compiler____
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
spike pk sum1ton.o
riscv64-unknown-elf-objdump -d 1_to_N.o | less (in new tab)
```
## Spike Simulation





## Write a C program for Signed And Unsigned Numbers 



```
vim unsignedHighest.c
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c
spike pk unsignedHighest.o
```





## For the signed number 




```
vim signedHighest.c
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signedHighest.o signedHighest.c
spike pk signedHighest.o
```

</details>

<details>
  <summary> Week 1 : Day 2 - Introduction to ABI and Basic Verification Flow </summary>
  <br>

# Introduction to ABI and basic verification flow

### Download the load.S , 1to9_count.c files from 
https://github.com/kunalg123/riscv_workshop_collaterals/tree/master/labs




```
cat 1to9_custom.c
cat load.S
```






```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.S
spike pk 1to9_custom.o
riscv64-unknown-elf-objdump -d 1to9_custom.o | less
```

## Spike Simulation

![Screenshot from 2023-08-21 09-10-32](https://github.com/ramdev604/pes_asic_class/assets/43489027/64e49c93-a6e6-42f4-a187-1c789809ce21)
</details>


### Week 2

<details>
  <summary>Day 1 : Introduction to Verilog RTL design and Synthesis
</summary>

  ## Task 1 : Loading and verifying functionality of a design.

  * After installation of tools run these commands to verify a design.

  ```bash
    sudo -s
    cd /VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    iverilog good_mux.v tb_good_mux.v
    ./a.out
    gtkwave tb_good_mux.vcd
  ```
  ![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/dcb825d3-6e07-417e-8f1f-61cae1baf730)

  **gtkwave simulation**
  
  ![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/1e684563-1204-4286-80e6-4b942f309654)

  ## Task 2 : Labs using Yosys and Sky130 PDKs.

  * Run there commands in the required folder.

  ```bash
  yosys
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog good_mux.v
  synth -top good_mux 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
  ```
  ![4](https://github.com/saneeaman9/pes_asic_class/assets/75088597/10bcbe8b-708c-4286-b991-3ac649634181)

  ![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/b25b3f47-a1ee-49ed-b098-38497d3a194b)

  </br>

  * Writing a netlist.
    ```bash
    write_verilog good_mux_netlist.v 
    !gvim good_mux_netlist.v

    write_verilog -noattr good_mux_netlist.v 
    !gvim good_mux_netlist.v 
    ```
  
  </br>

  * Simplified netlist.






  
  
</details>


<details>
  <summary>Day 2</summary>

  ### Task 1

    ```bash
     vim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    ```
  ![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/11a09ee1-5608-4ff9-842d-6dc1e9b19520)

  ![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/3394a377-bd16-4fab-ae4b-ba09c93326cf)

  ![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/e8c20cbe-3bdb-4546-9e2e-5d10fb941946)

  ![4](https://github.com/saneeaman9/pes_asic_class/assets/75088597/7c62a951-15c6-4427-86f5-7e2b4959c0bd)





  ### Task 2

  **Systhesis**

  ```bash
  yosys
read_liberty -lib ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
```
![6](https://github.com/saneeaman9/pes_asic_class/assets/75088597/77f01800-b5a2-47e5-961f-75d4759ac852)

![5](https://github.com/saneeaman9/pes_asic_class/assets/75088597/8380fa74-755f-4939-94c1-03fdfc4df31e)


```bash
write_verilog multiple_modules_hier.v
!vim multiple_modules_hier.v 
```
![7](https://github.com/saneeaman9/pes_asic_class/assets/75088597/594cc847-0123-4f1a-a208-6d496ca6a582)


### Task 3

  **Various Flop Coding Styles and optimization**

  * For async reset.
  
  ```bash
  iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd 
  ```

  ![8](https://github.com/saneeaman9/pes_asic_class/assets/75088597/d02386d3-cdf2-4814-a77f-73e424bbd6c3)


  * For async set

  ```bash
  iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
  ```

  ![9](https://github.com/saneeaman9/pes_asic_class/assets/75088597/07a8f950-b776-4b0e-9171-0179d9e1b4c4)


### Task 4

**Systhesizing all 3 codes**

```bash
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

1

```bash
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

2

```bash
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

3
</details>


<details>
  <summary>Day 3</summary>
  s
</details>
