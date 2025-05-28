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
