# Machine Learning

In Keras, the typical workflow involves creating a model, adding layers, compiling the model, training it with data, and then testing and using it. However, there are variations depending on the complexity of the model and the specific use case. Here’s a detailed explanation of the standard workflow and its applicability:

### Standard Workflow

1. **Create a Model**:
   
   - Define the architecture of the neural network by creating a model. This can be done using the Sequential API for simple models or the Functional API for more complex architectures.

2. **Add Layers**:
   
   - Add layers to the model to build the architecture. In the Sequential API, layers are added one after another. In the Functional API, layers can be added in a more flexible manner, allowing for shared layers, branching, and other complex structures.

3. **Compile the Model**:
   
   - Specify the optimizer, loss function, and metrics to monitor during training. This step configures the learning process.

4. **Train the Model**:
   
   - Fit the model to the training data using the `fit` method. This involves feeding the model with data and adjusting weights based on the loss function.

5. **Evaluate the Model**:
   
   - Assess the model’s performance on a test set using the `evaluate` method. This step helps in understanding how well the model generalizes to new data.

6. **Make Predictions**:
   
   - Use the trained model to make predictions on new data using the `predict` method.

## Example

```python
import numpy as np
import math
import tensorflow as tf
from keras import Sequential, layers
import matplotlib.pyplot as plt

rng = np.random.default_rng()

x_value = rng.uniform(low=0, high=(2*math.pi), size=10000)
y_value = np.sin(x_value) + (0.1 *rng.random(size=10000))
x_validation, x_test, x_training = x_value[0:2000], x_value[2000:4000], x_value[:]
y_validation, y_test, y_training = y_value[0:2000], y_value[2000:4000], y_value[:]

# plt.plot(x_validation, y_validation, 'r.', label = "Validation")
plt.plot(x_test, y_test, 'g.', label = "test")
# plt.plot(x_training, y_training, 'b.', label = "training")
plt.legend()


# Create Model
model = Sequential()

# Add layers to the model
model.add(layers.Dense(16, activation='relu', input_shape=(1,)))
model.add(layers.Dense(16, activation='relu'))
model.add(layers.Dense(1))

# Look at the summary of the model (optional)
model.summary()

# Compile model with right optimizer, loss function and metrics to model
model.compile(optimizer='rmsprop', loss='mae', metrics=['mae'])

# Train the model
trained_model = model.fit(x_training, y_training, epochs=500,
                           batch_size=100)


# Evaluate the trained model with test data
loss_val, metric_val = model.evaluate(x_validation, y_validation)

# Use the model to predic using the unknown data
predicted_y = model.predict(x_test)
plt.plot(x_test, predicted_y, 'r.')


plt.show()

# save the model in to a .h5 file
model.save('sine.h5')
```

## Calculating loss

![](C:\Users\jeeva\AppData\Roaming\marktext\images\2024-06-21-08-35-44-image.png)

Loss is measured using the simple technique where we square the distance between the predicted and actual value, add them up, then get the square root of the added result. 

Squaring up the distances makes sure that the negetive and positive distances dont cancel up with each other.
