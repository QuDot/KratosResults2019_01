# VMResults

Here we present results from classical simulations of Shor's Algorithm for the C++17 Implementation of the [QuDot Virtual Machine Specification] (http://www.qudotinc.com/QuDotIR.pdf?v2pdf=QuDotVM) called KratosVM. Raw output is in ```.out``` files. The plots were all generate by the ```process_shor.py``` python script. The process_shor script performs the classical post-processing steps of Shor's Algorithm and examines the probability distribution.

To run the script and generate a plot:
```python3 process_shor.py -N 731 -x 426 -k 19 -l 10 -s -f ~/shor50/shor731_426_500K.out```

* ```-N```: the number being factored (731)
* ```-x```: the random number used in the period finding algorithm f(z) = x^z mod N (426)
* ```-k```: size in qubtis of the control register (19)
* ```-l```: size in qubits of the input register (10)
* ```-s```: save plot to same location as out file
* ```-f```: location of input file

The number of qubits is determined as follows: if we wish to factor a number N then

* the lower input register ```l = ceil[log2(N)]```
* the upper control register ```k => ceil[log2(N^2)] < k <= floor[log2(2*N^2)]``` k is usually either ```2l``` or ```2l-1```
* quantum arithmetic (such as multiplcation which is used in Shor's Algorithm) requires ```2l+1``` qubits. These qubits are managed by the virtual machine when an arithmetic bytecode is encountered and not declared by the user.

For example, to factor ```N=731``` we have ```l=10``` therefore ```k=19``` and arithmetic requires ```2*l + 1 = 21```qubits. Therefore a total of ```10+19+21=50``` qubits is required.

We have results from 35,40,50,55,60 and 70 qubits which are in the respective folders.

Different numbers may be factored in each qubit folder, for example, in the shor60_e16 we factor both 2291 and 2573. Those results are in the factor2291 and factor2573 folders respectively. Within each factor<N> folder we have a file of the form ```shor<N>_<x>_<E>.out``` . N is the number being factored. x is the random number in period finding algorithm. E is the sample size for measurements. If E=500K then we took 500_000 samples to analyze. The ```src/``` folder  contains the VM bytecode program used. This program needs to be compiled and run on the virtual machine to give output.

