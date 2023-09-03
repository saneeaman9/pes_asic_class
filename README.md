
# PES_ASIC_Class



## Installation of the riscv tool

 -> Install by running these commands in terminal.

```bash
  git clone https://github.com/kunalg123/riscv_workshop_collaterals
cd riscv_workshop_collaterals
chmod 755 run.sh
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

![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/f940444d-260f-47a7-bc22-a656a2854321)


```bash
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/b2bfb0f9-af02-4a50-8797-ac8a9644ecc7)


```bash
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/d05b8cd7-70f0-4565-b885-dc94e48cf250)

</details>


<details>
  <summary>Day 3 : Combinational and sequential optmizations</summary>
  
  ### Task 1 Combinational logic optimizations

   ![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/527877b0-45c3-4307-8c4b-2c14078edd8f)


    ```bash 
    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog opt_check.v
    synth -top opt_check 
    opt_clean -purge
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show
    read_verilog opt_check2.v
    synth -top opt_check2
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
    show
    ```

   ![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/6e7349c4-1dc1-4885-aa42-ab34dda3b4ea)

   ![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/cb434a5c-0c95-4f02-9cd7-02f0b08fe375)

    
*Synthesis*
</br>

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
read_verilog opt_check4.v
synth -top opt_check4
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![4](https://github.com/saneeaman9/pes_asic_class/assets/75088597/6c515ee8-c8a0-414e-84da-4ec07599d3e8)

![5](https://github.com/saneeaman9/pes_asic_class/assets/75088597/ccc1c53d-8ea2-4966-b862-fd6eef262e60)


### Task 2 : Sequential Logic Optimizations

![6](https://github.com/saneeaman9/pes_asic_class/assets/75088597/68b02ecf-346c-43f6-b0e9-aaf914635828)


*Synthesis*

```bash
vim dff_const1.v -o dff_const2.v
iverilog dff_const1.v  tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
iverilog dff_const2.v  tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd 
```
![7](https://github.com/saneeaman9/pes_asic_class/assets/75088597/f3787239-029e-409d-9314-1d19bb8854d9)

![8](https://github.com/saneeaman9/pes_asic_class/assets/75088597/ebcd95d9-3b9e-407f-95a5-3b4b7a7cb7a6)

</br>

*Synthesis*

```bash
  yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/9a6b245e-deb6-4715-86d2-010ac0a36628)


*Synthesis*

```bash
read_verilog dff_const2.v
synth -top dff_const2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/453fe0a2-5f8c-4ae2-a319-04227691898d)


*GTKWave*

```bash
  iverilog dff_const3.v tb_dff_const3.v
  ./a.out
  gtkwave tb_dff_const3.vcd 
```

![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/a58e99df-c6d8-482f-91bb-a770b7e14f22)

*Synthesis*

```bash
  yosys
  read_verilog dff_const3.v
  synth -top dff_const3
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show  
```

![4](https://github.com/saneeaman9/pes_asic_class/assets/75088597/56d4c345-c487-4c6b-9611-79372ebc9107)


### Task 3 : Sequential logic optimizations for unused outputs

  *Synthesis*

  ```bash
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog  counter_opt.v
  synth -top counter_opt
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show  
  ```
  ![5](https://github.com/saneeaman9/pes_asic_class/assets/75088597/e72541a3-477c-4559-8297-b7ce830cb6b4)


  ```bash
  cp counter_opt.v counter_opt2.v
  vim  counter_opt2.v
  ```

  ![6](https://github.com/saneeaman9/pes_asic_class/assets/75088597/e669f0c0-e5ed-4674-9697-c92d975a2eb0)


  ```bash
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog counter_opt2.v
  synth -top counter_opt
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.li
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
  ```

![7](https://github.com/saneeaman9/pes_asic_class/assets/75088597/78c5fec2-8c05-44eb-9a6d-22dd2a278615)
</details>


<details>
  <summary>Day 4 : GLS, blocking vs non-blocking and Synthesis-Simulation mismatch</summary>

  ### Task 1

    ```bash 
      vim ternary_operator_mux.v -o bad_mux.v -o good_mux.v
      iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
      ./a.out
      gtkwave tb_ternary_operator_mux.vcd
    ```

   ![1](https://github.com/saneeaman9/pes_asic_class/assets/75088597/cba57d76-f6a0-4fb2-87bb-41474b8b97de)


   ![2](https://github.com/saneeaman9/pes_asic_class/assets/75088597/9c5d388b-502b-4136-9964-1cc4601cb565)


    ```bash
      iverilog bad_mux.v  tb_bad_mux.v
      ./a.out
      gtkwave tb_bad_mux.vcd
    ```
  

  ![3](https://github.com/saneeaman9/pes_asic_class/assets/75088597/73a3fa80-3a3b-4dbe-9974-daef82891ba4)


  __Synthesize bad_mux.v using yosys and generate a bad_mux_net.v netlist__

  __Now simulate using iverilog__

</details>
