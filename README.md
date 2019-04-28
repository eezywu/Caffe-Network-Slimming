# Network Slimming for Caffe
Network Slimming (Caffe) (ICCV 2017)

Application example
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

