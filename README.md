# qserver

**1.1 Classical vs. Quantum (The case for quantum)**



**2.1 Qserver**

**2.2 Flowchart**

**3.1 IBM Qiskit Implmentation**

IBM Qunatum Machines (ALL): https://quantum-computing.ibm.com/services?skip=0&systems=all

Maximum Available qubits for free:  5
Max qubits on a Simulator: 5000

**3.2 Grover's Algorithm**

The Grover's Search algorithm is a quantum algorithm for searching an unsorted database with N entries in $O(\sqrt{N})$ time. Classically, it would take O(N) time where we would need to search all entries in order to find the desired one. While this is only a quadratic speedup, it is quite significant when $N$ is large.

Given an unsorted list of $N$ elements, Grover's algorithm allows us to find a target element (in our case, a state) with $O(\sqrt N)$ operations or iterations. The reason why Grover's algorithm works so well (at least in theory) is because of its amplitude amplification, meaning it will single out the desired element without us having to search all the elements of the list.

**4.1 AWS Braket implementation try**



Sample Token: tok_1IHe3yAf0FnMgOaca3bOjzky

Sample APIs: 
GET /get/<user_id>
GET /check/<user_id>/<token>
POST /store {user_id: <user_id>, token: <token> }



{'qiskit-terra': '0.16.4',
 'qiskit-aer': '0.7.6',
 'qiskit-ignis': '0.5.2',
 'qiskit-ibmq-provider': '0.12.1',
 'qiskit-aqua': '0.8.2',
 'qiskit': '0.24.0'}


These are described by the following unitary evolution,

<img src="https://latex.codecogs.com/gif.latex?U_f&space;\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x,&space;f(x)\right\rangle." title="U_f&space;\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x,&space;f(x)\right\rangle." />

Here <img src="https://latex.codecogs.com/gif.latex?\left|x&space;,&space;\bar&space;0&space;\right\rangle&space;=&space;\left|x&space;\right\rangle&space;\otimes&space;\left|\bar&space;0&space;\right\rangle" title="\left|x , \bar 0 \right\rangle = \left|x \right\rangle \otimes \left|\bar 0 \right\rangle" />
 is used to represent a multi-qubit state consisting of two registers. The first register is in state  
|x⟩, where  x is  is a binary representation of the input to our function. The number of qubits in this register is the number of bits required to represent the inputs.



We acknowledge the use of IBM Quantum services for this work. The views expressed are those of the authors, and do not reflect the official policy or position of IBM or the IBM Quantum team.
