# AWS EC2 intance Cheatsheet

## AWS Server
### Connect to AWS Server
```
ssh -i {path/to/.pem key file} ubuntu@{Public DNS} 
```

### Transfer Files
#### To Server
```
scp -i {path/to/.pem key file} {path/to/file in your computer} ubuntu@{Public DNS}:/home/ubuntu/{path/to/dir to paste in server}
```
#### From Server
```
scp -i {path/to/.pem key file} ubuntu@{Public DNS}:/home/ubuntu/{path/to/file in server} {path/to/dir to paste in your computer} 
```

## Jupyter Notebook
### Run Notebook
```
jupyter notebook --ip=0.0.0.0 --no-browser
```
### Run in screen mode (keep task running if connection loss)

- Basically you run `screen`, run the command that you want, and then run `Ctrl + a + d` to detach from the session. You can then disconnect from the server/close the terminal and come back to it whenever you want by running `screen -r`.

## TensorFlow GPU setup
### Check for GPU in EC2 instance system
```
lspci | grep -i nvidia
```
### Install CUDA and cuDNN
To run Tensorflow with GPU support, we need to install the Nvidia CUDA and cuDNN. As of this writing these are the latest versions supported by Tensorflow ([link with instructions for installation](https://www.tensorflow.org/install/gpu))
### Add variables to `~/.bashrc`
```
export CUDA_HOME=/usr/local/cuda-8.0
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
export PATH=${CUDA_HOME}/bin:${PATH}
```
### Check Status
Execute `nvidia-smi` to display information about the GPU status
### Install tensorflow-gpu
```
pip install tensorflow-gpu
```
## TensorBoard
### Run TensorBoard
```
tensorboard --logdir={path/to/files} --host=0.0.0.0 --port=8080 
```
