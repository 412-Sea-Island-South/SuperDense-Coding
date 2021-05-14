🦈 The Superdense Coding Protocol!🦈
=====================================
What is the Superdense Coding Protocol?
---------------------------------------
In this project, I explored the world of Quantum Cryptography, and learned about the Superdense Coding Protocol.
The SDC Protocol is a type of Quantum Cryptography, in which two classical bits of information are trabsmitted using one qubit.
This is like a flipped version of Quantum teleportation, which you can read about [here](https://qiskit.org/textbook/ch-algorithms/teleportation.html).
Quantum Teleportation is the process of transmitting one qubit using two classical bits;
it's basically like destroying the quantum state of a qubit and recreating it elsewhere.
There are three steps to the Superdense Coding Protocol, which are
1. *Preparation*
2. *Encoding*
3. *Decoding*
   
How It Works
------------
### Step One: Preparation
A third party prepares two qubits in the entangled state (superposition).
Entanglement is when knowing the state of one qubit can help us deduce the state of the second.
They also prepare a third qubit, which will be the messenger
(i.e it sends the two bits of classical information).
All three qubits start in the |0⟩ state.  
Next, to entangle the two qubits, we apply a Hadamard gate to the first qubit and a CNOT gate to the first and second qubits.
This creates the Bell Pair (a superposition) and completes **Step 1**.
If you want to learn about quantum gates and operations, [go to this page](https://tksmax.github.io/Project1).
It also teaches you how to create a superposition, so it's a two in one package.
