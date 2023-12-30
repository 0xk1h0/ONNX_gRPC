### Distributed System Topics
### ECE5654_41

### Serving Machine Learning Model using ONNX with gPRC!
---
[![demo](https://youtu.be/naYlCwZX6Mg/0.jpg)](https://youtu.be/naYlCwZX6Mg)
---
- Environment : MacBook-Pro / Kernel Version 22.2.0 T6000 arm64 / Python 3.11.2

1. About ONNX
   - ONNX is an extension of the Open Neural Network Exchange, an open ecosystem that enables AI developers to choose the right tools as their projects evolve. ONNX provides an open source format for AI models, both deep learning and traditional ML. All deep learning libraries can use ONNX to convert to Tensorflow so they can use Tensorflow serving, but what about traditional machine learning like a tree based algorithm? Although it can be converted to ONNX, but tree based algorithm coming from xgboost or sklearn still cannot be converted to deep learning library (maybe in the future).

2. Requirements
  - numpy
  - scikit-learn
  - xgboost
  - onnxmltools
  - onnx
  - grpcio
  - onnxruntime

Based on that requirements, we need onnx runtime to run onnx inference, even though onnx has compatibility with some runtime like GraphPipe from Oracle which uses flatbuffers or Nvidia with its tensor rt and many more but what I will discuss here is the onnx runtime that comes from onnx itself.

Real world learning machines need more than a single inference. We need low latency in online or mini-batch inferences. In this tutorial I use dataset digits and xgboost to get the model.

The first step that must be done is to start the docker container from the onnx runtime server, port 9001 for http and 50051 for grpc while model_path is model_path in the docker

GRPC is available on localhost and port 50051. To call service methods, we first need to create a stub. We instantiate the PredictionServiceStub class of the prediction_service_pb2_grpc module from prediction_service.proto.

For RPC methods that return a single response (“response-unary” methods), gRPC Python supports both synchronous (blocking) and asynchronous (non-blocking) control flow semantics A synchronous call to the simple RPC Predict is nearly as straightforward as calling a local method. The RPC call waits for the server to respond, and will either return a response or raise an exception:

### How to usage.

0. `git clone` this repository.

1. Run `train.ipynb` to generate onnx format model file.

2. Run `run_ort_server.sh`
   1. You need to make sure you already have Docker installed.

3. Run `grpc_client_example.py` 
   1. It would be return the inference results (Label & Score).
