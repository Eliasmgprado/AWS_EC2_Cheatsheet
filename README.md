# AWS EC2 intance Cheatsheet

## Jupyter Notebook
### Run Notebook
```
jupyter notebook --ip=0.0.0.0 --no-browser
```
### Run in screen mode (keep task running if connection loss)

- Basically you run `screen`, run the command that you want, and then run `Ctrl + a + d` to detach from the session. You can then disconnect from the server/close the terminal and come back to it whenever you want by running `screen -r`.

## Tensor Board
### Run TensorBoard
```
tensorboard --logdir={path/to/files} --host=0.0.0.0 --port=8080 
```
