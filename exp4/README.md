## CODE
```
import numpy as np

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def sigmoid_derivative(x):
    return x * (1 - x)

# XOR problem
X = np.array([[0,0], [0,1], [1,0], [1,1]])
y = np.array([[0], [1], [1], [0]])

np.random.seed(42)
weights_input_hidden = np.random.uniform(size=(2, 4))
weights_hidden_output = np.random.uniform(size=(4, 1))
lr = 0.5

for epoch in range(10000):
    # Forward pass
    hidden_activation = sigmoid(np.dot(X, weights_input_hidden))
    output = sigmoid(np.dot(hidden_activation, weights_hidden_output))

    # Backward pass
    error = y - output
    d_output = error * sigmoid_derivative(output)

    error_hidden = d_output.dot(weights_hidden_output.T)
    d_hidden = error_hidden * sigmoid_derivative(hidden_activation)

    # Weight updates
    weights_hidden_output += hidden_activation.T.dot(d_output) * lr
    weights_input_hidden += X.T.dot(d_hidden) * lr

print("Predictions after training:")
print(np.round(output, 3))
```
## OUTPUT
```
Predictions after training:
[[0.04 ]
 [0.975]
 [0.972]
 [0.014]]
```
