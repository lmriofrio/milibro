---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# 4. ¿Por qué necesitamos computadoras cuánticas?

Cuando los científicos e ingenieros se enfrentan a problemas difíciles, recurren a las supercomputadoras. Estas son computadoras tradicionales muy grandes, a menudo con miles de núcleos de CPU y GPU clásicos. Sin embargo, incluso las supercomputadoras luchan por resolver ciertos tipos de problemas.

Si una supercomputadora se paraliza, probablemente se deba a que se le pidió a la gran máquina tradicional que resolviera un problema con un alto grado de complejidad. Cuando las computadoras tradicionales fallan, a menudo se debe a la complejidad.

#4.1 ¿Por qué las computadoras cuánticas son más rápidas?l

Una supercomputadora podría ser excelente realizando tareas difíciles como revisar una gran base de datos de secuencias de proteínas. Pero tendrá dificultades para ver los patrones sutiles en esos datos que determinan cómo se comportan esas proteínas.o:

```{code-cefrom qiskit import QuantumCircuit, Aer, transpile, assemble
from qiskit.visualization import plot_histogram
from qiskit.providers.aer import AerSimulator

# Definir el oráculo para el problema específico (en este caso, buscar el índice 5)
def oracle(circuit, register):
    circuit.cx(register[2], register[3])
    circuit.cx(register[0], register[3])
    circuit.cx(register[1], register[3])

# Implementar el algoritmo de Grover
def grover_algorithm():
    # Crear el circuito cuántico con 3 qubits
    grover_circuit = QuantumCircuit(4, 3)

    # Aplicar compuertas H a todos los qubits
    grover_circuit.h([0, 1, 2, 3])

    # Número de iteraciones recomendado para Grover para este problema específico
    num_iterations = 1

    # Aplicar el operador de Grover (oracle y difusión) iterativamente
    for _ in range(num_iterations):
        oracle(grover_circuit, [0, 1, 2, 3])
        grover_circuit.h([0, 1, 2, 3])
        grover_circuit.x([0, 1, 2, 3])
        grover_circuit.h(3)
        grover_circuit.mct([0, 1, 2], 3)
        grover_circuit.h(3)
        grover_circuit.x([0, 1, 2, 3])
        grover_circuit.h([0, 1, 2, 3])

    # Medir los primeros 3 qubits
    grover_circuit.measure([0, 1, 2], [0, 1, 2])

    return grover_circuit

# Ejecutar el algoritmo en un simulador cuántico
simulator = AerSimulator()
compiled_circuit = transpile(grover_algorithm(), simulator)
result = simulator.run(compiled_circuit, shots=1024).result()

# Visualizar los resultados
counts = resu/jupyterbook.org/file-types/jupytext.html).
```d:

```
jupyter-book myst init path/to/markdownfile.md
```
