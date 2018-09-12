# Object-Detection-Practice-using-CoLab
A step-by-step descriptions to show beginner to setup his first Object Detection project

We will follow the tutorial
https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10

  Setup the environment, prepare image data, and complete training on Google Colab environment. Training on Google Colab is 
almost 100 times faster than running on my Notebook (Lenovo X230, 12GB DRAM, with SSD)

# 1. Introduction
  The original project run the whole training on Windows-10 platform, with nVidia graphics accellerations. However, my notebook is not  powerful and each training iteration takes about 30s (in EdjeElectronics's post, it took 0.19s per iteration). In order to speedup the training, I want to leverage the Google CoLab K80 GPU. The result shows it took 0.3s per iteration on CoLab, which is pretty good for me.

# 2. Create a CoLab project
Setup the project as Python 3, and enable GPU
Add a cell of code to test if GPU is successfully allocated when start execution.

## 2-1. Install necessary Python packages
  By using !pip command to install required Python packages in CoLab environment

    !pip install pillow
    !pip install lxml
    !pip install Cython
    !pip install matplotlib
    !pip install pandas
    !pip install opencv-python

## 2-2. Download Tensorflow Models source from github
  Create a root directory and download the source code from github

    COLAB_TOP = '/content'
    MY_TOPPATH = '/models'
    MODEL_TOP = COLAB_TOP+MY_TOPPATH
    %cd $COLAB_TOP

    !git clone https://github.com/tensorflow/models

## 2-3. Setup environment variables

      RESEARCH_DIR = MODEL_TOP+'/research'
      OBJDET_DIR = RESEARCH_DIR+'/object_detection'
      RESEARCH_SLIM_DIR = RESEARCH_DIR+'/slim'

      %cd $OBJDET_DIR
      %env PYTHONPATH=$MODEL_TOP:$RESEARCH_DIR:$RESEARCH_SLIM_DIR

      import sys
      sys.path.append(RESEARCH_SLIM_DIR)

## 2-4. Install Protobuf
  a good reference regarding protobuf installation, you can refer to
https://stackoverflow.com/questions/48663207/colaboratory-install-tensorflow-object-detection-api

     !apt-get install -y -qq protobuf-compiler python-pil python-lxml
      %cd $RESEARCH_DIR
      !protoc object_detection/protos/*.proto --python_out=.
 
## 2-5. Run builder test

      %cd $RESEARCH_DIR
      %run object_detection/builders/model_builder_test.py

## 2-6.

      %cd $RESEARCH_DIR
      %run setup.py build
      %run setup.py install

## 2-7. sizeChecker.py

      %cd $OBJDET_DIR
      !wget 'https://raw.githubusercontent.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10/master/sizeChecker.py'
      %run sizeChecker.py --move










