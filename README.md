# RISC-V on Logisim

Implementation of a 32-bit two-cycle processor based on RISC-V using logisim-evolution.

## File Tree

Check if you already have the following files after pulling.

```
.
├── README.md
├── alu.circ
├── autolab.txt
├── cpu.circ
├── cpu-sanity.sh
├── cpu-user.sh
├── create_test.py
├── logisim-evolution.jar
├── mem.circ
├── regfile.circ
├── run.circ
├── my_tests
│   ├── circ_files
│   │   └── ...
├── tests
│   ├── circ_files
│   │   └── ...
│   ├── input
│   └── └── ...
└──  venus-jvm-latest.jar
```

## Sanity Tests

Six sanity tests include: CPU-addi.circ, CPU-add_lui_sll.circ, CPU-mem.circ, CPU-branch.circ, CPU-br_jalr.circ, and CPU-jump.circ. You can see the .s files and hex corresponding to each of these tests in the tests/input directory. Run them using the following command from the main directory:

```
$ ./cpu-sanity.sh
```
There is a Python script to make it a bit easier to interpret your test output. It's called binary_to_hex.py. It is in the tests/circ_files directory. You can run it on the reference output for CPU-addi.circ with the following command:
```
$ python binary_to_hex.py reference_output/CPU-addi.out
```
or, on the CPU's output with the following command:
```
$ python binary_to_hex.py output/CPU-addi.out
```
## Creating your tests

1. Write your tests and name them whatever you would like, but be sure to save them as .s files
2. Don't move the tests anywhere, keep them (as well as create_test.py) in the root directory of the project
3. Run:
```
$ python create_test.py <test 1 name here>.s <test 2 name here>.s ...
```
The file hierarchy should now contain some new things:
```
root
-- <test name here>.s  # Your test
-- my_tests
  -- circ_files
    -- <alu, cpu, mem, regfile>.circ  # All the circuits
    -- output
    -- reference_output
    -- CPU-<test name here>.circ  # The new circuit containing your test
  -- input
    -- <test name here>.hex  # The hex dissasembly of your test
    -- <test name here>.s  # A copy of your test
```
Now that everything is created, to test your own tests, run:
```
$ ./cpu-user.sh
```