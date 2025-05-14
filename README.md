# Computer Science Thesis: Quantum Tic-Tac-Toe

### Introduction
Quantum computers have the potential to vastly outperform classical computers by leveraging quantum mechanics to solve problems in unique and more efficient ways. Instead of using bits like a classical computer to store and transmit information, quantum computers use quantum bits, or *qubits*, that are physically realized as two-state quantum systems. The principles of quantum mechanics used in quantum computers are superposition, entanglement, interference, and decoherence. Qubits can represent a *superposition*, or linear combination, of states, which allows quantum computers to process multiple inputs simultaneously. *Entanglement* enables qubits to become strongly correlated, so that the state of one qubit depends on the state of another, no matter how far apart they are. Multiple entangled qubits prepared in a superposition of states experience *interference*, where the qubit states behave like waves, and the higher probability states are amplified. Measurement of a quantum system results in *decoherence*, which is when the quantum states collapse into definite values that can be interpreted by a classical computer. Decoherence can also occur unintentionally due to interactions with the surrounding environment. In quantum computers, qubits are first placed in a superposition of the computational basis states. They are then manipulated by a quantum circuit that creates entanglement, leading to interference among possible outcomes. This interference amplifies the correct solutions, which can then be extracted through measurement. This computational model has inspired great interest in applications where quantum computers may outperform classical ones, including factoring large numbers, simulating quantum materials, and solving complex optimization problems more efficiently. 

---

### Qiskit
Qiskit is an open-source SDK for quantum computing developed by IBM. It allows the user to build quantum circuits, transpile and optimize their quantum circuits for specific hardware backends, and execute their quantum circuits on real IBM quantum hardware or through a quantum simulator. 

When a quantum circuit is built in Qiskit, the user defines a sequence of quantum gates applied to qubits, similar to how logic gates are applied to bits in classical circuits. These quantum gates are high-level abstractions of operations that manipulate the state of the qubits according to the principles of quantum mechanics. After the circuit is created, it is passed through a transpiler, which optimizes the circuit and adapts it to match the topology of the chosen backend. This process includes decomposing high-level gates into the basis gates supported by the chosen quantum hardware, optimizing the circuit depth, and mapping the logical qubits to physical qubits that can be connected according to the hardware topology.

Once transpiled, the circuit is submitted to the chosen quantum backend. On an IBM quantum computer, this backend consists of a cryogenically cooled chip where superconducting circuits are manipulated by precise microwave pulses. These pulses are carefully shaped and timed to perform the desired quantum gate operations. Throughout this process, the system must minimize noise and environmental interactions to avoid decoherence. After the circuit has been executed, the qubits are measured, collapsing their quantum states into classical bits. The measurement results are then returned to the user for interpretation. If the circuit is run on a simulator backend instead, the entire computation is performed classically, allowing for ideal or noisy simulations depending on the selected model.

---

### Quantum Tic-Tac-Toe
I will be using Qiskit to construct a game of tic-tac-toe that utilizes the quantum circuit functionality, and is also able to be run on an IBM quantum computer or simulator. Like normal tic-tac-toe, each turn you place an X or an O in an unoccupied cell. Unlike normal tic-tac-toe, after each turn, you have the option to place a quantum gate on any initialized cell. The game runs until all cells are initialized, and then the user has the option to measure the final results on a real IBM quantum computer or on a simulator. When the final game is measured, the most likely output is returned, and a winner is determined based on normal tic-tac-toe rules

---

### Use Cases

#### Use Case 1.1: Classical Move
- **Actors**: Player X or Player O  
- **Overview**: Player chooses an uninitialized cell on the classical board to place an X or O.

**Typical Course of Events**:
- Player takes their normal turn by claiming an unoccupied cell on the classical board to place an X or O.  

**Alternative Courses**:
- **Player chooses to quit the game**:  
  - Program exits
- **If the cell is already initialized**:  
  - Show error.  
  - Allow the player to reselect an uninitialized cell.

#### Use Case 1.2: Qubit Flip
- **Actors**: Player X or Player O  
- **Overview**: Player places a Pauli X gate on an initialized cell to flip its state from X to O or O to X.

**Typical Course of Events**:
- Player takes their normal turn by claiming an unoccupied cell.  
- Player chooses to apply an `X` gate to that cell.  
- Quantum circuit is updated with the `X` gate.

**Alternative Courses**:
- **If player skips the gate application**:  
  - Move ends normally.  
  - Proceed to the next player's turn.
- **If the cell is not initialized**:  
  - Show error.  
  - Allow the player to reselect an initialized cell.
 
---

#### Use Case 1.3: Superposition Move
- **Actors**: Player X or Player O  
- **Overview**: Player places a Hadamard gate on an initialized cell to put it into a superposition of X and O.

**Typical Course of Events**:
- Player takes their normal turn by claiming an unoccupied cell.  
- Player chooses to apply an `H` gate to that cell.  
- Quantum circuit is updated with the `H` gate.

**Alternative Courses**:
- **If player skips the gate application**:  
  - Move ends normally.  
  - Proceed to the next player's turn.
- **If the cell is not initialized**:  
  - Show error.  
  - Allow the player to reselect an initialized cell.

---

#### Use Case 1.4: Entangled Play
- **Actors**: Player X or Player O  
- **Overview**: Player applies a `CNOT` gate to entangle two cells, making their outcomes correlated.

**Typical Course of Events**:
- Player places a mark in an unoccupied cell.  
- Player selects two cells that have already been initialized.  
- Player applies a `CNOT` between the two cells.  
- Quantum circuit is updated with the `CNOT` gate.

**Alternative Courses**:
- **If no valid second cell is available**:  
  - Only offer single-qubit gates.
- **If player skips the gate application**:  
  - Move ends normally.  
  - Proceed to the next player's turn.
- **If one or both selected cells are uninitialized**:  
  - Show error.  
  - Allow the player to reselect cells.

---

#### Use Case 1.5: Swap Move
- **Actors**: Player X or Player O  
- **Overview**: Player uses a `SWAP` gate to exchange the quantum states of two initialized cells.

**Typical Course of Events**:
- Player places their mark on an unoccupied cell.  
- Player selects two previously initialized cells.  
- Player applies a `SWAP` gate between them.  
- Quantum circuit is updated with the `SWAP` gate.

**Alternative Courses**:
- **If no valid second cell is available**:  
  - Only offer single-qubit gates.
- **If player skips the gate application**:  
  - Move ends normally.  
  - Proceed to the next player's turn.
- **If one or both selected cells are uninitialized**:  
  - Show error.  
  - Allow the player to reselect cells.

---

#### Use Case 1.6: Phase Disruption
- **Actors**: Player X or Player O  
- **Overview**: Player uses a `Z` gate to apply a phase flip, potentially altering interference patterns.

**Typical Course of Events**:
- Player takes their normal turn by claiming an unoccupied cell.  
- Player chooses to apply an `Z` gate to that cell.  
- Quantum circuit is updated with the `Z` gate.

**Alternative Courses**:
- **If player skips the gate application**:  
  - Move ends normally.  
  - Proceed to the next player's turn.
- **If the cell is not initialized**:  
  - Show error.  
  - Allow the player to reselect an initialized cell.

---

#### Use Case 1.7: Quantum Final Measurement
- **Actors**: System  
- **Overview**: When all cells are initialized, the system runs the circuit on a simulator or real backend, then resolves the game.

**Typical Course of Events**:
- All 9 cells are initialized.  
- System prompts player to choose a backend: simulator or real IBM quantum computer.  
- Circuit is executed, results are sampled.  
- Most probable result is returned and displayed as the final board state.  
- Classic tic-tac-toe rules determine the winner.
