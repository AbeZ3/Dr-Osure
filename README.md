# Dr. Osure, Virtual AI Assistant

Dr. Osure, a virtual assistant made with a Jetson Nano and VS Code made at ID Tech camps in MIT Boston, Masachusetts.  he is intended to be a chatbot with the ability to recognize facial emotion, I am connecting his VS Code script to a Character AI software so he can "see" and "talk to us"

![add image descrition here](direct image link here)

![out1](https://github.com/user-attachments/assets/4afc0be1-d7f4-43ce-922f-9c35ce64d2cc)
![out2](https://github.com/user-attachments/assets/9daff936-e671-48f5-9da5-3127c8cef6ce)
![out3](https://github.com/user-attachments/assets/85804ab1-d171-4f3f-b44c-5660e434256f)
![out4](https://github.com/user-attachments/assets/fd064c74-1d0c-4dcf-b310-8e7cb03d15f4)



## The Algorithm
The algorithm powering Dr. Osure uses AI to recognize facial emotions in images. Through extensive training, the computer learns to identify specific emotional cues and classify them into different categories, such as happiness, sadness, anger, and surprise.


## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.


**Running the Project:**
To run this project, follow these steps:

1. **Set Up Your Environment:**
   - Open VS Code and connect to your Jetson Nano.
   - Ensure you have installed Jetson Inference and Docker Image from: [Jetson Inference](https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md).

2. **Prepare Your Files:**
   - Download the FER-2013 dataset and save it to your device. Ensure it is located in the `jetson-inference/python/training/classification/data` directory.

3. **Navigate to the Project Directory:**
   - Open a terminal and navigate to the project directory:
     ```bash
     cd nvidia/jetson-inference/
     ```

4. **Run the Docker Container:**
   - Run the Docker container:
     ```bash
     ./docker/run.sh
     ```
   - You may need to re-enter your NVIDIA password at this step.

5. **Set Up the Training Environment:**
   - From inside the Docker container, change directories to the training classification folder:
     ```bash
     cd jetson-inference/python/training/classification
     ```

6. **Train the Model:**
   - Run the training script to re-train the network:
     ```bash
     python3 train.py --model-dir=models/Emotions --data=data/FER2013
     ```
   - Specify the number of epochs and batch sizes if needed:
     ```bash
     python3 train.py --model-dir=models/Emotions --data=data/FER2013 --batch-size=32 --workers=4 --epochs=50
     ```
   - Training will take several hours depending on the number of epochs.

7. **Manage Training Sessions:**
   - You can stop the training at any time using `Ctrl+C` and resume later with the `--resume` and `--epoch-start` flags.

8. **Export the Model:**
   - Once training is complete, export the model to ONNX format:
     ```bash
     python3 onnx_export.py --model-dir=models/Emotions
     ```
   - Verify that the new model, `resnet18.onnx`, is in the `models/Emotions` folder.

9. **Test the Model:**
   - Exit the Docker container by pressing `Ctrl+D`.
   - On your Jetson Nano, navigate to the classification directory:
     ```bash
     cd jetson-inference/python/training/classification
     ```
   - Check the model file:
     ```bash
     ls models/Emotions/
     ```
   - You should see `resnet18.onnx` listed.

10. **Run Inference:**
    - Set the `NET` and `DATASET` variables:
      ```bash
      NET=models/Emotions
      DATASET=data/FER2013
      ```
    - Run the inference script to test the model on an image:
      ```bash
      imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/test_image.jpg TestImage1.jpg
      ```

**Dataset:**
The FER-2013 dataset used for training can be downloaded from [Kaggle](https://www.kaggle.com/datasets/msambare/fer2013?resource=download).

This process outlines how to set up, train, and run the Dr. Osure emotion-recognizing software on a Jetson Nano. By following these steps, you can develop a powerful tool for emotion detection and analysis.

---




[View a video explanation here](video link) 
