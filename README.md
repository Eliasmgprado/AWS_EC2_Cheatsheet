# AWS EC2 intance Cheatsheet
## Create Instance
- Go to AWS console page
- Click on **Instances**
- Click on **Launch Instance**
- On `Step 1: Choose an Amazon Machine Image (AMI)`, click on **AWS Marketplace**
- Search for **Deep Learning**
- Choose **AWS Deep Learning AMI**
- On `Step 2: Choose an Instance Type`, choose **p2.xlarge**
- On `Step 6: Configure Security Group`, Add following inbound rules:
    - Custom TCP	TCP	8888	0.0.0.0/0	| For jupyter notebook
    - Custom TCP	TCP	8080	0.0.0.0/0 | For tensorboard

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
- screen mode commands:
    - `Ctrl a c` - Creates a new screen session so that you can use more than one screen session at once.
    - `Ctrl a n` - Switches to the next screen session (if you use more than one).
    - `Ctrl a p`- Switches to the previous screen session (if you use more than one).
    - `Ctrl a d` - Detaches a screen session (without killing the processes in it - they continue).
    
    
### TMUX

1. run the command `tmux`
2. in the new shell that pops up, execute the job
3. detach from the tmux shell by using the shortcut `(Ctrl+b then d)`
4. if the ssh connection resets, ssh to the instance again and run `tmux attach`
5. the job should have kept on running and you can resume where you left off


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
