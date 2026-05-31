# Proto

This repository contains the gRPC Protobuf contracts for communication between the Java Hub and Python Classifier microservices.

## Directory Structure

```
/
├── README.md
└── classifier/
    └── v1/
        └── classifier.proto
```

## Classifier Contract

The `classifier/v1/classifier.proto` file defines the gRPC service for audio classification between the Java Hub and Python Classifier.

### Service Definition

- **AudioClassifier**: gRPC service for classifying audio frames
  - `Classify`: RPC method that accepts audio frame data and returns classification results

### Messages

- **AudioFrameRequest**: Contains sensor data including FFT bins, location, and audio metrics
- **ClassificationResponse**: Returns threat type, confidence score, and model version

## Consuming the Contract

### Java Hub

The Java Hub microservice uses the protobuf Gradle plugin to generate Java classes from this submodule.

### Python Classifier

The Python Classifier generates Python gRPC code using:

```bash
python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. classifier/v1/classifier.proto
```

## Backward Compatibility

**Do not modify existing fields.** To introduce breaking changes, create a new `v2/` directory following the same structure.