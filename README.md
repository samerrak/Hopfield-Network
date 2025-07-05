# Hopfield Networks

This repository contains an implementation and analysis of Hopfield Networks, completed as part of COMP 549: Brain Inspired AI, Winter 2025, by Samer Abdulkarim.

---

## 🧠 Overview

Hopfield Networks are recurrent neural networks that store patterns as attractors of a dynamical system. They can retrieve a stored pattern when presented with a noisy or partial version.

---

## 💡 Key Concepts

### Processing Units

- Neurons that can be in two states (+1 or −1), acting as binary units.

### State of Activation

- Vector representing the state of each neuron at a given time.

### Output Function

- Neuron fires (+1) if its input surpasses a threshold, otherwise it stays off (−1).

### Connectivity Pattern

- Symmetric weight matrix **W**, with zero self-connections (Wii = 0).

### Propagation Rule

- Neuron input is computed as:
```
net_i(t) = ∑_j W_ij o_j(t-1)
```

### Activation Rule

- Neuron state updates using its net input and threshold.

### Learning Rule

- **Hebbian learning rule**:
```
ΔW_ij = η o_i o_j
```
Strengthens connection if both neurons fire together.

### Environment

- The network minimizes an energy function, moving toward stable attractor states corresponding to stored patterns.

---

## ⚙️ Energy Function

The energy function guides convergence:
```
E(o) = -∑_i,j W_ij o_i o_j
```
Low-energy states correspond to stored patterns (memories).

---

## 💾 Implementation

### Key Functions

#### `store_one`

Stores a single pattern by updating weights using the Hebbian rule.

```python
def store_one(self, image, c=1):
    self.weight += c * np.outer(image, image)
    self.patternStored.append(image)
    self.weight /= len(self.patternStored)
    np.fill_diagonal(self.weight, 0)
    return self.weight
```

#### `store_multi`

Stores multiple patterns iteratively with gradient-based updates and normalization.

#### `update`

Synchronous update of neuron states over specified epochs, using net inputs and thresholds.

---

## 🖼️ Results

### One-Pattern Storage

- Successfully retrieves clean images from noisy inputs.
- Example: image with noise level 0.1 converges to original pattern.

### Multi-Pattern Storage

- Can recall multiple patterns, but higher noise or overlap increases retrieval errors.
- Example: images with noise level 0.2 show partial retrieval and mixed states.

---

## 📈 Visualizations

- Weight matrices show strengthened connections between co-active neurons.
- State trajectories demonstrate convergence to attractor states.
- Example figures included (see project figures in the repo).

---

## ✍️ Key Takeaways

- Hopfield Networks effectively store and retrieve binary patterns using associative memory.
- Capacity is approximately 0.15 * N (number of neurons).
- Retrieval quality depends on noise level and pattern similarity.
- Hebbian learning reinforces co-active neurons, inspired by "cells that fire together wire together."

---

## 📄 References

- Hopfield, J. J. (1982). Neural networks and physical systems with emergent collective computational abilities. *Proceedings of the National Academy of Sciences*.
- Course notes from COMP 549: Brain Inspired AI (Winter 2025).

---

## ✉️ Contact

Samer Abdulkarim  
[LinkedIn](https://www.linkedin.com/in/samerabdulkarim)  
Email: samer_ak@icloud.com

---

⭐ Feel free to fork, clone, or contribute!
