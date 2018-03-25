# hunter_dlib_ncnn
Test dlib -> caffe -> ncnn using hunter

### build

```
mkdir -p _builds/xcode 
mkdir -p _install/xcode
cmake -H. -B_builds/xcode -GXcode -DCMAKE_TOOLCHAIN_FILE=/path/to/polly/xcode.cmake  DCMAKE_VERBOSE_MAKEFILE=ON -DHUNTER_STATUS_DEBUG=ON -DCMAKE_INSTALL_PREFIX=_install/xcode
cmake --build _builds/xcode --config Release --target install --
```

### (optional) train model (metric_network_renset.xml)

```
_install/xcode/bin/dnn_metric_learning_on_images_ex johns
```

### convert model to caffe format using dlib tools

```
install/xcode/bin/convert_dlib_nets_to_caffe metric_network_renset.xml 1 3 150 150
```

Output:
```
Writing python part of model to metric_network_renset_dlib_to_caffe_model.py
Writing weights part of model to metric_network_renset_dlib_to_caffe_model.weights


*************** ERROR CONVERTING TO CAFFE ***************
No conversion between dlib pooling layer parameters and caffe pooling layer parameters found for layer 127
dlib_output_nc: 35
bottom_nc:      72
padding_x:      0
stride_x:       2
kernel_w:       3
pad_x:          1
```
