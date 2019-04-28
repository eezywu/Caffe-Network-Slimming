# A Caffe Re-Implementation of Network Slimming
This repository is the caffe re-implementation for the following paper  
[Learning Efficient Convolutional Networks Through Network Slimming](http://openaccess.thecvf.com/content_iccv_2017/html/Liu_Learning_Efficient_Convolutional_ICCV_2017_paper.html) (ICCV 2017).

## Note
You should add `optional float l1_lambda = 6 [default = 1e-9];` to in the the field of `message ScaleParameter` in `$(CAFFE_HOME)/src/caffe/proto/caffe.proto` file. I don't upload the `caffe.proto` directly, because the file is likely to contain your other modifications, and you need to be careful to replace it.

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
    l1_lambda: 0.001  # L1 regularization coefficient for gamma
  }
}
```

## Contact
eezywu@gmail.com
