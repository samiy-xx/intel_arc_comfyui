# intel_arc_comfyui
Instructions on how to install comfy ui for intel arc for  ubuntu 23



On a fresh ubuntu 23 install do the following
follow instructions here https://github.com/vladmandic/automatic/wiki/Intel-ARC

`sudo apt update && sudo apt install -y ca-certificates wget gpg`

`wget -qO - https://repositories.intel.com/gpu/intel-graphics.key | sudo gpg --dearmor --output /usr/share/keyrings/intel-graphics.gpg`

`echo "deb [arch=amd64,i386 signed-by=/usr/share/keyrings/intel-graphics.gpg] https://repositories.intel.com/gpu/ubuntu jammy client" | sudo tee /etc/apt/sources.list.d/intel-gpu-jammy.list`

`sudo apt update && sudo apt upgrade -y`

`sudo apt-get install intel-opencl-icd intel-level-zero-gpu level-zero git python3-pip python3-venv libgl1 libglib2.0-0 libgomp1 libjemalloc-dev`

git clone comfy
cd into comfy

`python3 -m venv venv`

`source venv/bin/activate`

`pip install torch==2.1.0a0 torchvision==0.16.0a0 intel-extension-for-pytorch==2.1.10+xpu --extra-index-url https://pytorch-extension.intel.com/release-whl/stable/xpu/us/`

`pip install mkl==2024.0.0 mkl-dpcpp==2024.0.0`

`pip install -r requirements.txt`

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/comfy/venv/lib/`


run comfy with 

`nice -n 19 ipexrun xpu main.py --highvram --use-pytorch-cross-attention --bf16-unet --bf16-vae`

this makes comfy run. Atleast i was able to use sdxl and sdxl turbo, control net and some  depth map and canny nodes.
ip-adapter, instantid and reactor was a crash



