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
  
### Step Two: Encoding
Now that we have prepared everything, it's time for the action to begin.
This is where we distribute the entangled pair to our sender and reciever, who I will creatively name S and R.
There are a few rules for encoding (and later decoding) the message.
This is just one example of the many different possible rules.
<h4 align="center">Encoding Rules</h4>
<table style="width:100%" align="center">
   <tr>
      <th>Intended Message</th>
      <th>Gates</th>
      <th>Result ⨉ √2</th>
   </tr>
   <tr>
      <td>00</td>
      <td>I (Identity)</td>
      <td>|00⟩ + |11⟩</td>
   </tr>
   <tr>
      <td>01</td>
      <td>X (NOT)</td>
      <td>|01⟩ + |10⟩</td>
   </tr>
   <tr>
      <td>10</td>
      <td>Z (Pauli-Z)</td>
      <td>|00⟩ - |11⟩</td>
   </tr>
   <tr>
      <td>11</td>
      <td>ZX</td>
      <td>-|01⟩ + |10⟩</td>
   </tr>
</table>
  
### Step 3: Decoding
Now that R has recieved S's qubit, he uses his entangled qubit to decode the message.
In order to do this, he simply reverses the gates which the third party entangled.
In other words, first R applies a CNOT, followed by a H gate.
And of course, there are rules for decoding as well.
<h4 align="center">Decoding Rules</h4>
<table width="100%" align="center">
   <tr>
      <th>Recieved State</th>
      <th>After CNOT</th>
      <th>Final Result</th>
   </tr>
   <tr>
      <td>|00⟩ + |11⟩</td>
      <td>|00⟩ + |01⟩</td>
      <td>|00⟩</td>
   </tr>
   <tr>
      <td>|01⟩ + |10⟩</td>
      <td>|11⟩ + |10⟩</td>
      <td>|01⟩</td>
   </tr>
   <tr>
      <td>|00⟩ - |11⟩</td>
      <td>|00⟩ - |01⟩</td>
      <td>|10⟩</td>
   </tr>
   <tr>
      <td>-|01⟩ + |10⟩</td>
      <td>-|11⟩ + |10⟩</td>
      <td>-|11⟩ = |11⟩</td>
   </tr>
</table>
<p align="center">
   Learn how to code this in Qiskit!
   <a href="https://studentsxstudents.com/superdense-coding-sdc-c31a9661c3cd">Learn how to code this in Qiskit!</a>
</p>
