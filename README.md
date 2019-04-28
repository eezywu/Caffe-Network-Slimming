# A Caffe Re-Implementation of Network Slimming
This repository is the caffe re-implementation for the following paper  
[Learning Efficient Convolutional Networks Through Network Slimming](http://openaccess.thecvf.com/content_iccv_2017/html/Liu_Learning_Efficient_Convolutional_ICCV_2017_paper.html) (ICCV 2017).

## Attention
You should manually modify the code in `$(CAFFE_HOME)/src/caffe/proto/caffe.proto` as follows. 
```
message ScaleParameter {
  optional int32 axis = 1 [default = 1];
  optional int32 num_axes = 2 [default = 1];
  optional FillerParameter filler = 3;
  optional bool bias_term = 4 [default = false];
  optional FillerParameter bias_filler = 5;
  optional float l1_lambda = 6 [default = 1e-9];  // The code that you need to add manually.
 }
```
I didn't upload the `caffe.proto` directly, because the file is likely to contain your other modifications, and you need to be careful to replace it.

## Application example
```
layer {
  name: "conv1/scale"
  type: "Scale"
  bottom: "conv1/bn"
  top: "conv1/bn"
  scale_param {
    filler {
      value: 0.5
    }
    bias_term: true
    bias_filler {
      value: 0
    }
    l1_lambda: 0.0001  // The L1 regularization coefficient for gamma
  }
}
```

## Contact
eezywu@gmail.com
