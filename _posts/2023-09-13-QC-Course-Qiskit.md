---
layout: post
title: Basic Quantum Computing - Getting started with Qiskit
author: Charles Thomas
---

Now, we've learnt a little bit about quantum computing let's get started by programming one.

## Python
We're going to be using the Python programming language to start writing quantum programmes. So I'm going to assume you know a little bit of Python and have it installed locally.

I'm also going to assume that you have a little bit of knowledge of how to use the terminal (or command prompt on Windows).

So let's start by creating a folder to store our quantum programs:

```
mkdir QuantumPrograms && cd QuantumPrograms
```

Now let's setup a virtual environment. This means all the libraries we install will only be used for this project.

To do this run:

```
python3-m venv ./venv
source venv/bin/activate
```

Finally, let's install Qiskit which is the libary we'll use to start working with Quantum Computers.

```
pip install qiskit
pip install qiskit_aer
```

## Writing our first quantum program

Let's create a file called `first_quantum_programme.py` and let's add the following contents:

```
from qiskit import QuantumCircuit, QuantumRegister, transpile
from qiskit_aer import AerSimulator
```

These two lines are going to import all the things we'll need for writing our program.

Next let's add:

```
register = QuantumRegister(1)
circuit = QuantumCircuit(register)
```

This creates a quantum register with 1 qubit. (A quantum register is just a collection of qubits).  In Qiskit, all registers start with all the qubits set to 0. It then creates a circuit containing our register

Now let's add: 

```
circuit.x(register[0])
```

This line applies an X gate (e.g. a NOT gate) to the first qubit in our register

Now we can add
```
circuit.measure_all()
```

This will measure all the qubits in our circuit

Finally, let's add:

```
simulator = AerSimulator()

compiled_circuit = transpile(circuit, simulator)

job = simulator.run(compiled_circuit, shots=1000)

result = job.result()
counts = result.get_counts(compiled_circuit)

print(counts)
```

This will create a simulator that simulates a quantum computer. It will then take our circuit and convert into a form that the simulator can understand. Then it will run a 1000 times theon simulator. Finally, we get the results of running our programme on the simulator.

So in total our programme should look like this:

```
from qiskit import QuantumCircuit, QuantumRegister, transpile
from qiskit_aer import AerSimulator


register = QuantumRegister(1)
circuit = QuantumCircuit(register)

circuit.x(register[0])

circuit.measure_all()

simulator = AerSimulator()

compiled_circuit = transpile(circuit, simulator)

job = simulator.run(compiled_circuit, shots=1000)

result = job.result()
counts = result.get_counts(compiled_circuit)

print(counts)

```

Now we can run it using the following command:

```
python3 first_quantum_programme.py
```

And we should get the following output: 

```
{'1': 1000}
```

This tells we got the result 1 a thousand times which is exactly what we'd expect because we started with a qubit set to 0 then applied a NOT gate to change it to a 1.

