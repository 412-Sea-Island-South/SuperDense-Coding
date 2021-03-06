🦈 The Superdense Coding Protocol!🦈
=====================================
  
<h2>What is the Superdense Coding Protocol?</h2>
In this project, I explored the world of Quantum Cryptography, and learned about the Superdense Coding Protocol.
The SDC Protocol is a type of Quantum Cryptography, in which two classical bits of information are transmitted using one qubit.
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
   <a href="https://studentsxstudents.com/superdense-coding-sdc-c31a9661c3cd">Learn how to code this in Qiskit!</a>
</p>
  
#### Reference Materials: Qiskit Code
```python
# import everything for ease
from qiskit import *
from qiskit.visualization import *
from random import randint

def create_bell_pair(qc, a, b):
    qc.h(a) #H-gate
    qc.cx(a,b) #CNOT-gate
    
def encode_message(qc, qubit, msg):
    if msg == "00":
        pass    #do nothing
    elif msg == "10":
        qc.x(qubit) #X-gate
    elif msg == "01":
        qc.z(qubit) #Z-gate
    elif msg == "11":
        qc.z(qubit) #Z-gate
        qc.x(qubit) #X-gate
    else:
        print("Invalid Message!")
        
def decode_message(qc, a, b):
    qc.cx(a,b) #CNOT-gate
    qc.h(a) #H-gate
    
#Create the quantum circuit with 2 qubits
qc = QuantumCircuit(2)
#third party prepares entangled state
create_bell_pair(qc, 0, 1)

qc.barrier() #adds barrier to make circuit look nicer
#A encodes A's message onto qubit 0
message = ["00", "01", "10", "11", "I'd like a Double Big Mac Please!"][randint(0,4)] #choose a random message
print("Message is", message) #what is the message?
encode_message(qc, 0, message)
qc.barrier()
# A the sends qubit to B
#B applies the recovery protocol
decode_message(qc, 0, 1)
#B measures qubits to read A's message
qc.measure_all()
#Draw our output
qc.draw()

qasm_sim = Aer.get_backend('qasm_simulator')
qobj = assemble(qc)
result = qasm_sim.run(qobj).result()
counts = result.get_counts(qc)
plot_histogram(counts)
```
  
#### Reference Materials: Gallery
<h4 align="center">A sample SDC Circuit</h4>
<p align="center">
  <img src="https://user-images.githubusercontent.com/81530826/118306185-e6cd2000-b49d-11eb-9394-d9d06e330907.png">
</p>
<h4 align="center">SDC Circuit Simulation</h4>
<p align="center">
  <img src="https://user-images.githubusercontent.com/81530826/118306411-43c8d600-b49e-11eb-8421-3569cb56882a.png">
</p>
  
## About Me
Hello there! I'm Max, an innovator at [The Knowledge Society aka TKS](https://tks.world).
I'm interested in a lot of different emerging technologies, but my main interests right now are Quantum Computing ⚛️, Blockchain 💵, Artificial Intelligence 🤖, and last but not least, Space Tech/Exploration 🚀.
So yeah, that's basically who I am. You can check out my social media profiles below.  
<p>
  <a href="https://www.linkedin.com/in/max-cui-p18051/" rel="nofollow noreferrer">
    <img src = "https://i.stack.imgur.com/gVE0j.png" alt="linkedin">
    LinkedIn
  </a> &nbsp;
  <a href = "https://github.com/TKSMax" rel="nofollow noreferrer">
    <img src = "https://i.stack.imgur.com/tskMh.png" alt="github">
    GitHub
  </a> &nbsp;
  <a href="https://max-c.medium.com" rel="nofollow noreferrer">
    Medium
  </a> &nbsp;
  <a href = "https://maxmcui.substack.com" rel="nofollow noreferrer">
    Sub to my Newsletter
  </a>
  <a href="https://tksmax.github.io/FocusProjects" rel="nofollow noreferrer">
    Back to Main Page
  </a>
</p>
