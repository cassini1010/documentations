# PyTorch

## torchvision

### Object detection models

- `fasterrcnn_mobilenet_v3_large_320_fpn`

- `fasterrcnn_mobilenet_v3_large_fpn`

- `fasterrcnn_resnet50_fpn`

- `fasterrcnn_resnet50_fpn_v2`

- `fcos_resnet50_fpn`

- `retinanet_resnet50_fpn_v2`

- `retinanet_resnet50_fpn`

## Model building in PyTorch

Modle building in pytorch is certerd around two classes in `torch.nn` module.

- torch.nn.Module : contains models and its componets such as nural network layers

- torch.nn.Parameter: comprises of lerning weights

## Layers

Linear Layer

Convolutional Nural network Layer (CNN)

Recurrent Nural network Layer (RNN)

Transformers : These are teh multi pursose nural networks mostly used for NLP

### other layerrs and funciton

#### Max pooling and Min pooling

Reduces the size of the tensor by combining cells together and assigning the maximum/minimum value of the input cell respectively to the output cell respectively.

## Autograd in PyTorch

`Autograd` is the differentianion engine in pytorch. 

```python
import torch

# Step 1: Create a tensor with requires_grad=True
x = torch.tensor(2.0, requires_grad=True)

# Step 2: Define a function (computational graph)
y = x**2 + 3*x + 4   # y = x² + 3x + 4

# Step 3: Backpropagate
y.backward()  # Computes dy/dx

# Step 4: Check the gradient
print(x.grad)  # Output: tensor(7.)
```

### Math Involved

$$
y=x^2+3x+4

$$

> Taking differentiation of an expression and equating it to zero gives the minima of the function.

$$
\frac{d}{dx}=2x+3
$$

Since tensor has value of 2.0

$$
\frac{d}{dx} = 2*2+3 = 7
$$

`x.grad` also gave `7` as output.

> Often weights and biases are manually updatde in each iteration by calculating the difference between the predicted value and the actual value. Hence often differentiation of loss w.r.t weight and bias are done

$$
\frac{ꝺ}{ꝺweight}loss
$$

$$
\frac{ꝺ}{ꝺ bias}loss
$$

### Example

If the model is Linear, the prediction is done using linear expression (equation of a straight line).

w = weight

b = bias

Y = actual value

yp = predicted value

$$
y_p=wx+b
$$

You want to **learn the best `w` and `b`** that minimize the error between predicted price and actual price. This error is captured by the **loss function**:

$$
Loss=\frac{1}{n} \sum_1^n(y_{prediction}−Y)^2
$$

To reduce the loss, you must update `w` and `b` **in the right direction**. This is where **gradients (derivatives)** help:

- The **derivative tells you the slope** of the loss function w.r.t. each parameter.

- Using **gradient descent**, you update parameters like this:

$$
w=w-lr*(ꝺloss/ꝺw)
$$

$$
b=b-lr(ꝺloss/ꝺb)
$$

`lr` is the learning rate. Weight/bias is reduced if gradiant is positive and is increased if gradiant is negative.

```python
import torch

# Sample data: house size vs price
X = torch.tensor([[1.0], [2.0], [3.0], [4.0]])
Y = torch.tensor([[3.0], [5.0], [7.0], [9.0]])

# Parameters to learn: w (weight), b (bias)
w = torch.randn(1, requires_grad=True)
b = torch.randn(1, requires_grad=True)

# Learning rate
lr = 0.01

# Training loop
for epoch in range(1000):
    # Forward pass
    y_pred = X * w + b
    loss = ((y_pred - Y) ** 2).mean()

    # Backward pass
    loss.backward()

    # Update weights manually
    with torch.no_grad():
        w -= lr * w.grad
        b -= lr * b.grad

        # Zero the gradients
        w.grad.zero_()
        b.grad.zero_()

    # Print progress
    if epoch % 100 == 0:
        print(f"Epoch {epoch}: Loss = {loss.item():.4f}, w = {w.item():.4f}, b = {b.item():.4f}")
```



## Training a model manually

Consider below input(X) and expected output(Y), stating with a random weight and bias 0.0. Note that predeined weight and bias can be anything.

```python
X = numpy.array([1,2,3,4,5], dtype=numpy.float32)
Y = numpy.array([6, 11, 16, 21, 26], dtype=numpy.float32)
# weights and bias
pre_weight = 0.0
pre_bias = 0.0
```

Define a linear regression model of expression `y=mx+c` in the forward method. This is the model that we are going to train and bring the weights and bias towards perfection.

Loss function gives out mean squared value of difference between prediction and actual expected value.

Backward function computes the differentiation of the loss function and finds the minima of weight and bias respectively.

Loss function:

$$
Loss = \frac{1}{n}\sum_1^n(y_{predicted}-y_{actual})^2

$$

Expanding ` Y prediction` gives:

$$
Loss = \frac{1}{n}\sum_1^n(w*X+b-y_{actual})^2
$$



Minima of loss functoin w.r.t weight:

$$
\frac{d}{dw}Loss=\frac{1}{n}\sum_1^n2(w.X+b-y_{actual})*X
$$

Minima of loss function w.r.t bias:

$$
\frac{d}{db}Loss=\frac{1}{n}\sum_1^n2(w.X+b-y_{actual})
$$

Updating of the weights and biases are done using below expression:

$$
weights = weights - (lerningRate*\frac{d}{dw}Loss)
$$



$$
Bias= Bias- (lerningRate*\frac{d}{db}Loss)
$$

Below is the code for all the steps mentioned above

```python
# model prediction
def forward(input, w, b):
    return w*input+b

# loss function
def loss(prediction, actual):
    return ((prediction-actual)**2).mean()

# calculate Gradiant
def backward(input, prediction, actual):
    weight_grad = numpy.dot(2*input, prediction-actual).mean()
    bias_grad = numpy.dot(2, prediction-actual).mean()
    return weight_grad, bias_grad

def update_weight_bias(w, b, lr, dw, db):
    updated_weight = w - (lr*dw)
    updated_bias = b -(lr*db)
    return updated_weight, updated_bias
```



Training of the model is done in 10000 epochs as shown below

```python
for i in range(10000):
    y_prediction = forward(X, pre_weight, pre_bias)
    # print(f" Predicted y is {y_prediction}")
    loss_value = loss(y_prediction, Y)
    # print(f"Calculated loss is {loss_value}")
    wgrad, bgrad = backward(X, y_prediction, Y)
    # print(f"weight gradiant is {wgrad} and bias gradiant is {bgrad}")
    pre_weight, pre_bias = update_weight_bias(pre_weight, pre_bias, 0.01, wgrad, bgrad)
    # print(f"updated weight  {pre_weight} and updated bias is {pre_bias}")

print(f"updated weight  {pre_weight} and updated bias is {pre_bias}")

```
