# Architecture of Neural Network

Source article: [Architecture Of Neural Network - Rajeswari P (Medium)](https://medium.com/@rajeswari19p/architecture-of-neural-network-c65cf8624a0d)

This note captures the core ideas of the post in a concise, study-friendly format.

## Prerequisite Context

Before this topic, the author recommends understanding:

- Perceptron
- Sigmoid neuron

These are foundational units that lead into full neural network architectures.

## Why Architecture Matters

Neural network architecture defines how information flows from raw input to prediction. A typical network includes:

- Input layer: receives user/data features.
- Hidden layer(s): transforms features using weights, biases, and activation functions.
- Output layer: produces final prediction/classification.

In short:

- Leftmost layer = input neurons
- Rightmost layer = output neuron(s)
- Middle layers = hidden neurons

"Hidden" is only a structural term: those neurons are neither in input nor output layers.

## From Single Hidden Layer to MLP

A network can have one hidden layer or multiple hidden layers.

When there are multiple hidden layers, the model is called a Multi-Layer Perceptron (MLP).

### Multi-Layer Perceptron (MLP)

An MLP is a feedforward neural network with:

- Multiple layers of neurons
- Nonlinear activation functions

Why this matters:

- Nonlinearity helps model complex relationships.
- Deeper representations can solve harder real-world tasks.

## Practical MLP Examples

Real-world examples mentioned:

- Spam email filtering
- Handwritten digit recognition
- Facial recognition
- Stock price prediction

## MLP in Action: Spam Filter

How the flow works conceptually:

1. Input layer:
	- Email text is converted into numeric features (for example, frequencies or embeddings).
2. Hidden layers:
	- The network learns feature interactions and patterns that separate spam from legitimate emails.
3. Output layer:
	- Produces a binary decision: spam or not spam.

## Digit Classification Illustration

The post also illustrates digit detection (e.g., deciding if an image is the digit "9").

Example setup:

- If the image size is 64 x 64 grayscale, input neurons = 4096.
- Each input neuron represents one pixel intensity scaled to [0, 1].
- A single output neuron can represent confidence for "is 9".
- A threshold (for example, 0.5) can convert output to class decision.

The author also references hidden-layer heuristics to balance model capacity and training effort.

## Feedforward Neural Network (FNN)

A feedforward network passes signals only in one direction:

- Layer $L_i$ output becomes layer $L_{i+1}$ input.
- No cycles/instant feedback loops.

This forward-only topology keeps computation straightforward and stable for many tasks.

## Recurrent Neural Network (RNN)

RNNs introduce feedback over time:

- Outputs from earlier time steps can influence later processing.
- Temporal dependencies are preserved through recurrent connections.

Key idea from the post:

- Feedback is delayed across time steps, not immediate self-dependence in the same instant.

This makes RNNs useful for sequence-based problems.

### RNN Advantages Highlighted

- Strong for sequential/temporal data
- Useful where context over time matters
- Applied to tasks such as:
  - Speech recognition
  - Language modeling
  - Time-series style prediction

## Quick FNN vs RNN Comparison

| Aspect | FNN | RNN |
|---|---|---|
| Information flow | One-way, input to output | Includes recurrent temporal feedback |
| Memory of past inputs | No explicit sequence memory | Maintains context over time |
| Typical data | Static/tabular/image features | Sequential data (text, speech, signals) |

## Core Takeaways

- Neural architecture determines learning behavior and representational power.
- MLPs (multiple hidden layers + nonlinearity) can model complex patterns.
- FNNs are clean forward pipelines.
- RNNs are built for temporal dependencies and sequential context.

## Mentioned Next Step in the Post

The article points to a follow-up on building a simple handwritten-digit classifier.

