# qserver

##Classical vs. Quantum (The case for quantum)
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
