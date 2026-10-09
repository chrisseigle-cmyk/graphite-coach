# Line drawing model

`lines.onnx` is the "anime style" generator from **Informative Drawings: Learning to generate line drawings that convey geometry and semantics** (Caroline Chan, Frédo Durand, Phillip Isola, CVPR 2022), https://github.com/carolineec/informative-drawings, MIT License, Copyright (c) 2022 Caroline Chan.

The ONNX export comes from https://github.com/Kazuhito00/Informative-Drawings-ONNX-Sample (MIT License). Its weights were converted to 16-bit floats to halve the download; inputs and outputs stay 32-bit. Input: `input_image` [1,3,512,512] RGB in 0..1. Output: [1,1,512,512], where 1 is white paper and 0 is ink.

`vendor/` holds onnxruntime-web 1.30.0 (MIT License, Microsoft), which runs the model in the browser.

# Background removal model

`cutout.onnx` is **U^2-Net** (small, `u2netp`) from *U^2-Net: Going Deeper with Nested U-Structure for Salient Object Detection* (Xuebin Qin et al., Pattern Recognition 2020), https://github.com/xuebinqin/U-2-Net, Apache-2.0 License. The ONNX build is the one published by the rembg project (https://github.com/danielgatis/rembg, MIT License), sha256 309c8469258dda742793dce0ebea8e6dd393174f89934733ecc8b14c76f4ddd8. Input: `input.1` [1,3,320,320], RGB scaled to 0..1 then normalised with mean (0.485, 0.456, 0.406) and standard deviation (0.229, 0.224, 0.225). The first of its seven outputs is the one used: [1,1,320,320], higher where the pixel belongs to the subject.

# Face landmarks

`face.task` is Google's **MediaPipe Face Landmarker** (float16, version 1), https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker, Apache-2.0 License, sha256 64184e229b263107bc2b804c6625db1341ff2bb731874b0bcc2fe6544e0bc9ff. It finds 478 points on a face, including the irises, and is used to place the darkest accents (pupils, nostrils, lip line) in step 8. When it finds no face (a pet, for example), the plan falls back to dark spots read from the drawing.

`vendor/mediapipe/` holds `@mediapipe/tasks-vision` 0.10.14 (Apache-2.0 License, Google): `vision_bundle.js` (the package's `vision_bundle.mjs`, source-map comment removed) and the SIMD WebAssembly runtime `vision_wasm_internal.js` / `.wasm`.
