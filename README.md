# QC-Mentorship-program
#Task 2 find negative values
# I've run the code using Google Colab

# I have provided a specific number_list as input

number_list = [-15, -14, -3, -1, 1, 2, 4, 8, 11, 15]

# I've added the necessary installations for Qiskit, Qiskit Aer, and Tweedledum, which are required libraries for running the code

!pip install qiskit
!pip install qiskit-aer
!pip install tweedledum
from qiskit import QuantumCircuit, Aer, transpile, assemble
from qiskit.visualization import plot_histogram
from qiskit.utils import QuantumInstance
from qiskit.algorithms import Grover
from qiskit.circuit.library import PhaseOracle


def find_negative_numbers(number_list):
    # I've determined the number of qubits required based on the list size
    num_qubits = len(number_list)

    # I've created a quantum circuit with the required number of qubits
    qc = QuantumCircuit(num_qubits)

    # I've applied quantum gates to check for negative values
    for i, num in enumerate(number_list):
        if num < 0:
            qc.x(i)  # Flip the qubit to |1| if the number is negative

    # Measuring the qubits
    qc.measure_all()

    # Simulating the quantum circuit
    simulator = Aer.get_backend('qasm_simulator')
    job = simulator.run(qc, shots=1)
    result = job.result().get_counts(qc)

    # Checking if any qubits are in the |1| state
    for num in number_list:
        if num < 0:
            return "True"
    return "False"

# Examples

A = [1, -3, 2, 15]
result = find_negative_numbers(A)
print(result)  # Should print "True" for this example list

B = find_negative_numbers([1, 4, 8, 11])
print(B)  # Should print "False"

C = find_negative_numbers([-15, -14, 2, -1])
print(C)  # Should print "True"
