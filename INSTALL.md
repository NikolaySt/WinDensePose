# Denseponse and Detectron for Windows
## How to configure, build and run in several simple steps.

The installation process will create a standalone environment.

### Step one
- Make a local copy  of the repository and all sub-modules.

### Step two
Setup WinPython643.6.8 Zero
 - Create a new sub-folder WPy64 in the repository 
 - Download it from here https://sourceforge.net/projects/winpython/files/WinPython_3.6/3.6.8.0/WinPython64-3.6.8.0Zero.exe/download
 - Install in WPy64

### Step three
 - Download densepose_uv_data from the url https://dl.fbaipublicfiles.com/densepose/densepose_uv_data.tar.gz
 - Unzip the files and copy them in densepose\DensePoseData\UV_data.

### Step four
 - Install the latest VS2019 from here https://visualstudio.microsoft.com
The installation has to include Python language support, MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.23).

### Step five
#### Installing all python packages which we will need to run densepose.
 - First option: Open Densepose.sln from the main folder with Visual Stuiod. From Visual Stuiod -> Solution Explorer -> Python environments select WinPy64 then open the context menu click ``Install from requirements``

 - Second option: From windows go to WinPy64 folder start ``WinPython Command Prompt.exe`` then got to ``densepose`` folder and run: ``pip install -r requirements.txt``

### Step six
#### Build and install cocoapi and detectron
 - From windows go to WinPy64 folder start ``WinPython Command Prompt.exe``
 - Then in the console follow these steps:
   1. go to folder ``cocoapi\PythonAPI`` and run the following command:
      - python setup.py build
      - python setup.py install
   2. go to folder ``densepose`` and run the following command:
      - python setup.py build
      - python setup.py install      

### Step eight
#### Inference with Pretrained Models.
If all of the previous steps succeed then we can test whether everything is working properly. 

#### Option one:
  1. Open Densepose.sln with  Visual Studio then run the project: 

#### Option two:
   1. From windows explorer go to WinPy64 folder start ``WinPython Command Prompt.exe``
   2. Go the main folder and run setpath.bat this will set up the following python path: ``set PYTHONPATH=%cd%\densepose;%PYTHONPATH%``
   3. Go to ``densepose`` folder and run one of these commands: 
```
python tools/infer_simple.py --cfg configs/DensePose_ResNet101_FPN_s1x-e2e.yaml --output-dir DensePoseData/infer_out/ --image-ext jpg --wts https://dl.fbaipublicfiles.com/densepose/DensePose_ResNet101_FPN_s1x-e2e.pkl DensePoseData/demo_data/demo_im.jpg
```
or 
```
python tools/infer_simple.py --cfg configs/DensePose_ResNet50_FPN_s1x-e2e.yaml --output-dir DensePoseData/infer_out/ --image-ext jpg --wts https://dl.fbaipublicfiles.com/densepose/DensePose_ResNet50_FPN_s1x-e2e.pkl DensePoseData/demo_data/demo_im.jpg
```

- The output in the console will contain many lines but these will confirm that everything is working:
             
      INFO infer_simple.py: 111: Inference time: 2.606s
      INFO infer_simple.py: 114:  | im_detect_bbox: 2.154s
      INFO infer_simple.py: 114:  | misc_bbox: 0.000s
      INFO infer_simple.py: 114:  | im_detect_body_uv: 0.452s
      INFO infer_simple.py: 117:  \ Note: inference on the first image will be slower than the rest (caches and auto-tuning need to warm up)
      IUV written to:  DensePoseData/infer_out/demo_im_IUV.png

## For more additional details you can read densepose and detectron documentations

### In addition
There are there scripts you can run to download some files:
densepose\DensePoseData
get_DensePose_COCO.sh
get_densepose_uv.sh
get_eval_data.sh
To run .sh scripts Install cygwin => https://cygwin.com/setup-x86_64.exe

In Step three we download some files by hand from get_densepose_uv.sh