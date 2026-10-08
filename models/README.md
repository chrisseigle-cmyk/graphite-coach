# Line drawing model

`lines.onnx` is the "anime style" generator from **Informative Drawings: Learning to generate line drawings that convey geometry and semantics** (Caroline Chan, Frédo Durand, Phillip Isola, CVPR 2022), https://github.com/carolineec/informative-drawings, MIT License, Copyright (c) 2022 Caroline Chan.

The ONNX export comes from https://github.com/Kazuhito00/Informative-Drawings-ONNX-Sample (MIT License). Its weights were converted to 16-bit floats to halve the download; inputs and outputs stay 32-bit. Input: `input_image` [1,3,512,512] RGB in 0..1. Output: [1,1,512,512], where 1 is white paper and 0 is ink.

`vendor/` holds onnxruntime-web 1.30.0 (MIT License, Microsoft), which runs the model in the browser.
