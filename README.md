
# Installation serverless YOLOv8 functions on Windows 10 with using the Ubuntu subsystem 

- Navigate to the directory ```"cvat/serverless/yolov8/nuclio"```. (If it does not exist, create it.) Copy the necessary files to the directory with the following command.

```bash
git clone https://github.com/zahidesatmutlu/custom-yolov8-model-cvat-auto-annotation
cd custom-yolov8-model-cvat-auto-annotation
```

- Update the ```"metadata/annotations/spec"``` section in the "function.yaml" file with the classes you trained the model with. For example:

```bash
metadata:
  name: custom-model-yolov8
  namespace: cvat
  annotations:
    name: custom-model-yolov8
    type: detector
    framework: pytorch
    # change this accordingly to your model output/classes
    spec: |
      [
        { "id": 0, "name": "car" },
        { "id": 1, "name": "person" },
        { "id": 2, "name": "motorcycle" },
        { "id": 3, "name": "truck" }
      ]

```

- Copy your model weight in .pt format to the same directory (```"cvat/serverless/yolov8/nuclio"```). In "main.py" insert the model weight you trained in ```"model = YOLO('best.pt')"``` (Line 13).

- Go back to the ```"/cvat"``` directory and deploy the YOLOv8 functions.

```bash
./serverless/deploy_cpu.sh serverless/yolov8/
```

- Open Google Chrome browser and navigate to ```localhost:8080```. You can now view the custom YOLOv8 model for CVAT!

<p align="center">
  <img src="https://imgur.com/LA6cTEr" />
YOLOv8 model for CVAT
</p>
