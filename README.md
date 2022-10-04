# QuantumProgramming
## We can create a circuit in Quantum computers for half adder and full adder and many more
### we can also program a full-fledged software for quantum computers using this tool provided by IBM called Qiskit

Example 1 : *Half adder* uses two inputs and two outputs. it can only add two bits.(not really though...)
these are not bits but qubits
which can exist in simultaneous but different states... defined by *statevectors*.

```python
#creating a half adder quantum circuit
#using CNOT(Controlled NOT in Quantum or XOR)
#create circuit with 4 qubits and 2 classical bits
from qiskit import *
from qiskit.providers.aer import AerSimulator
qc=QuantumCircuit(4,2)
#since a qubit is initialized to 0 in its start state we flip it using .x() which is a quantum NOT gate
qc.x([0,1])
qc.cx(0,2)
qc.cx(1,2)
qc.ccx(0,1,3)
qc.measure([2,3],[0,1])
qc.draw()
job=sim.run(qc)
result=job.result()
result.get_counts()
#This is the circuit created : 

     ┌───┐                     
q_0: ┤ X ├──■─────────■────────
     ├───┤  │         │        
q_1: ┤ X ├──┼────■────■────────
     └───┘┌─┴─┐┌─┴─┐  │  ┌─┐   
q_2: ─────┤ X ├┤ X ├──┼──┤M├───
          └───┘└───┘┌─┴─┐└╥┘┌─┐
q_3: ───────────────┤ X ├─╫─┤M├
                    └───┘ ║ └╥┘
c: 2/═════════════════════╩══╩═
                          0  1 
#and the output for the addition of two qubits with fixed input 1 and 1 is :
{'10': 1024} # for 1024 counts...
```
Example 2 : We can also create a circuit for full-adder for adding three qubits
suppose q<sub>0</sub>, q<sub>1</sub>, q<sub>2</sub> all are 1
then creating the circuit as follows, 

```python
from qiskit import *
qfa=QuantumCircuit(5,4)
qfa.x([0,1,2])
qfa.cx([0,1,2],[3,3,3])
qfa.ccx(0,2,4)
qfa.ccx(0,1,4)
qfa.ccx(1,2,4)
qfa.measure([3,4],[0,1])
qfa.draw()
     ┌───┐                                    
q_0: ┤ X ├──■──────────────■───────■──────────
     ├───┤  │              │       │          
q_1: ┤ X ├──┼────■─────────┼───────■────■─────
     ├───┤  │    │         │       │    │     
q_2: ┤ X ├──┼────┼────■────■───────┼────■─────
     └───┘┌─┴─┐┌─┴─┐┌─┴─┐  │  ┌─┐  │    │     
q_3: ─────┤ X ├┤ X ├┤ X ├──┼──┤M├──┼────┼─────
          └───┘└───┘└───┘┌─┴─┐└╥┘┌─┴─┐┌─┴─┐┌─┐
q_4: ────────────────────┤ X ├─╫─┤ X ├┤ X ├┤M├
                         └───┘ ║ └───┘└───┘└╥┘
c: 4/══════════════════════════╩════════════╩═
                               0            1 
from qiskit.providers.aer import AerSimulator
sim = AerSimulator()
job=sim.run(qfa)
result=job.result()
result.get_counts()
{'0011': 1024}
```
