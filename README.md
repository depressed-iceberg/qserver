# qserver

Files:

Qserver_Grovers1 : 4 bit Implmenetation of Grover's algorithm using unitary quantum gates on Qasm Simulator and 5 bit IBM QC ibmq_belem + ibmq_lima

Qserver_Grovers2 : 5 bit implementation of Grover's algorithm using diffuser, oracle on statevector simulator and IBM QC ibmq_lima

Qserver_Shors: Implmenets Shor's algorithm to decrypt a sample number

**1.1 Classical vs. Quantum (The case for quantum)**



**2.1 Qserver**

The Qserver in this setup uses Quantum computing to Decrypt the token which is encrypted by classical RSA encryption algorithm by factorizing the public key value. The token in this case is a small number used for simplicity as factorizing large numbers would take a long time since I only have access to Shor being run on a simulator on a classical machine. This onviously isn't the case for a quantum machine.

(key, value) pairs can be stored using qubit registeres
for example: for a 4 qubit system, 2 qubit registeres (2^2) can be used to store 4 keys and 2 registers to store 4 values.


An actual circuit designed using Quirk (2 qubits for key, 2 for value and 5th to mark whether the value was found/not found):
[Link to circuit!](https://algassert.com/quirk#circuit=%7B%22cols%22:[[%22H%22,%22H%22],[%22%E2%80%A6%22,%22%E2%80%A6%22],[%22%E2%97%A6%22,%22%E2%97%A6%22,%22X%22,%22X%22],[%22%E2%80%A2%22,%22%E2%97%A6%22,1,%22X%22],[%22%E2%97%A6%22,%22%E2%80%A2%22],[%22%E2%80%A2%22,%22%E2%80%A2%22,%22X%22],[1,1,%22%E2%80%A6%22,%22%E2%80%A6%22],[1,1,%22%E2%97%A6%22,%22%E2%80%A2%22,%22X%22],[1,1,%22%E2%80%A6%22,%22%E2%80%A6%22],[1,1,1,1,%22Z%22],[1,1,%22%E2%80%A6%22,%22%E2%80%A6%22],[1,1,%22%E2%97%A6%22,%22%E2%80%A2%22,%22X%22],[%22%E2%80%A2%22,%22%E2%80%A2%22,%22X%22],[%22%E2%97%A6%22,%22%E2%80%A2%22],[%22%E2%80%A2%22,%22%E2%97%A6%22,1,%22X%22],[%22%E2%97%A6%22,%22%E2%97%A6%22,%22X%22,%22X%22],[%22H%22,%22H%22],[%22%E2%80%A6%22,%22%E2%80%A6%22],[%22X%22,%22X%22,1,1,%22X%22],[%22%E2%80%A2%22,%22%E2%80%A2%22,1,1,%22Z%22],[%22X%22,%22X%22,1,1,%22X%22],[%22%E2%80%A6%22,%22%E2%80%A6%22],[%22H%22,%22H%22],[%22%E2%97%A6%22,%22%E2%97%A6%22,%22X%22,%22X%22],[%22%E2%80%A2%22,%22%E2%97%A6%22,1,%22X%22],[%22%E2%97%A6%22,%22%E2%80%A2%22],[%22%E2%80%A2%22,%22%E2%80%A2%22,%22X%22],[1,1,%22%E2%97%A6%22,%22%E2%80%A2%22,%22X%22],[%22Chance2%22,1,%22Chance2%22,1,%22Chance%22]]%7D )

https://github.com/JoelLeach/QuantumDatabaseSearch

**2.2 Flowchart**

<img src="https://lucid.app/publicSegments/view/fe988690-165a-4560-94b5-8a47c35dd040/image.png"/>


Sample Token: tok_1IHe3yAf0FnMgOaca3bOjzky

Sample APIs: 
GET /get/<user_id>
GET /check/<user_id>/<token>
POST /store {user_id: <user_id>, token: <token> }

Sample Token used: 

**3.1 IBM Qiskit Implmentation**

Available IBM Quantum Machines (ALL): https://quantum-computing.ibm.com/services?skip=0&systems=all

Maximum Available qubits for free:  5
Max qubits on a Simulator: 5000

Development Specs: 
{'qiskit-terra': '0.16.4',
 'qiskit-aer': '0.7.6',
 'qiskit-ignis': '0.5.2',
 'qiskit-ibmq-provider': '0.12.1',
 'qiskit-aqua': '0.8.2',
 'qiskit': '0.24.0'}



**3.2 Grover's Algorithm**

The Grover's Search algorithm is a quantum algorithm for searching an unsorted database with N entries in $O(\sqrt{N})$ time. Classically, it would take O(N) time where we would need to search all entries in order to find the desired one. While this is only a quadratic speedup, it is quite significant when $N$ is large.

Given an unsorted list of $N$ elements, Grover's algorithm allows us to find a target element (in our case, a state) with $O(\sqrt N)$ operations or iterations. The reason why Grover's algorithm works so well (at least in theory) is because of its amplitude amplification, meaning it will single out the desired element without us having to search all the elements of the list.

Assumption: 1. That the Oracle has access to the elements(token values) of the classical list. 
2.That we can load with a superposition of addresses (token addresses) data from a RAM, also called QRAM. 

**Loading the values**

"<img src="https://latex.codecogs.com/gif.latex?|x\rangle_{\text{address}}|0\rangle_{\text{value}}&space;\rightarrow&space;|x\rangle_{\text{address}}|\textrm{load}(x)\oplus&space;0\rangle_{\text{value}}&space;=&space;|x\rangle_{\text{address}}|\textrm{load}(x)\rangle_{\text{value}}." title="|x\rangle_{\text{address}}|0\rangle_{\text{value}} \rightarrow |x\rangle_{\text{address}}|\textrm{load}(x)\oplus 0\rangle_{\text{value}} = |x\rangle_{\text{address}}|\textrm{load}(x)\rangle_{\text{value}}." />/>

And then
<img src="https://latex.codecogs.com/gif.latex?H^{\otimes&space;n}_{\text{address}}&space;|0\rangle_{\text{address}}|\textrm0\rangle_{\text{value}}=\frac1{2^{n/2}}\sum_{x=0}^{2^n-1}&space;|x\rangle_{\text{address}}|\textrm0\rangle_{\text{value}}" title="H^{\otimes n}_{\text{address}} |0\rangle_{\text{address}}|\textrm0\rangle_{\text{value}}=\frac1{2^{n/2}}\sum_{x=0}^{2^n-1} |x\rangle_{\text{address}}|\textrm0\rangle_{\text{value}}" />

<img src="https://latex.codecogs.com/gif.latex?\text{apply&space;load}\rightarrow\frac1{2^{n/2}}\sum_{x=0}^{2^n-1}&space;|x\rangle_{\text{address}}|\textrm{load}(x)\rangle_{\text{value}}/" title="\text{apply load}\rightarrow\frac1{2^{n/2}}\sum_{x=0}^{2^n-1} |x\rangle_{\text{address}}|\textrm{load}(x)\rangle_{\text{value}}/" />

Firts apply the _Hadamard gates_ on the address register and then apply the _load operation_ on both registers. Then you will have a superposition of all values in the database an the value register.

Next, apply GA on the value register with any oracle (think of it as an optimization function and what constraints it has; like looking a for a prime or a specific value). After 𝑂(√𝑁) iterations the correct answer will be measured with high probability. Thus, the correct solution together with the register address 𝑥∗ of the correct solution will be very likely measured.


**Steps for Grover's**

It is better to think of the quantum search algorithm as optimizing a function, instead of searching in a list/database. In an after thought, Grover's might not be the best algorithm for searching. 



These are described by the following unitary evolution,

<img src="https://latex.codecogs.com/gif.latex?U_f&space;\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x,&space;f(x)\right\rangle." title="U_f&space;\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x,&space;f(x)\right\rangle." />

Here <img src="https://latex.codecogs.com/gif.latex?\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x&space;\right\rangle&space;\otimes&space;\left|\bar&space;0&space;\right\rangle" title="\left|x , \bar 0 \right\rangle = \left|x \right\rangle \otimes \left|\bar 0 \right\rangle" />
 is used to represent a multi-qubit state consisting of two registers. The first register is in state  
|x⟩, where  x is  is a binary representation of the input to our function. The number of qubits in this register is the number of bits required to represent the inputs.


**Result**
FILE: Qserver_Grovers1.ipynb
& FILE: Qserver_Grovers2.ipynb 
Outputs from IBM computers in /images


**3.3 Shor's Algorithm** 


Note: this implementation of Shor’s algorithm uses 4𝑛+2 qubits, where 𝑛 is the number of bits representing the integer in binary. So in practice, for now, this implementation is restricted to factorizing small integers. Given the above value of N we compute 4𝑛+2 below and confirm the size from the actual circuit.

**AWS Braket implementation: Tried but free tier is very limited** (remove)


**Other Resources**
Microsoft Q# Qunatum Development Kit
Original paper for Grover's algorithm : https://arxiv.org/pdf/quant-ph/9706005.pdf

We acknowledge the use of IBM Quantum services for this work. The views expressed are those of the authors, and do not reflect the official policy or position of IBM or the IBM Quantum team.
