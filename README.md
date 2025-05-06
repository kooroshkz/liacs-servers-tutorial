# liacs-servers-tutorial
A brief tutorial on how to connect to LIACS servers using SSH - to be completed later in summer


# Neural-Computing-Group-Assignment
Group assignment for Neural Computing

### Run Venv for project
```bash
python3 -m venv nc_venv
source nc_venv/bin/activate
pip install torchvision==0.21.0 torch==2.6.0 notebook==7.3.3 ipykernel==6.29.5
```
#### Use conda for python 3.9+ (In case u faced the red error type)
```bash
conda create -y -p ./nc_venv python=3.9
conda activate ./nc_venv
pip install torchvision==0.21.0 torch==2.6.0 notebook==7.3.3 ipykernel==6.29.5

```
### If you are a Windows user (not recommended btw)
```bash
python -m venv nc_venv
nc_venv\Scripts\activate
pip install torchvision torch==2.6.0 --index-url https://download.pytorch.org/whl/cu126
pip install notebook==7.3.3 ipykernel==6.29.5
```

### How to connect to LIACS ds lab servers
```bash
ssh <stu_no>@ssh.liacs.nl
```
Then we have to jump to either `vibranium`(Two powerful GPU) or `duranium`(Multiple GPU) server
```bash
ssh vibranium # or ssh duranium
```
### Run in the background

#### with `Screen`
```bash
screen -S session_name
python model.py
Ctrl + A, then D
screen -r session_name
screen -list # to see the list of running screens
```

#### with `tmux`
```bash
tmux new -s Model
# detach with Ctrl-b then d
tmux attach -t Model    # re-attach later
tmux ls # list running screens
```



### Check GPU usage
```bash
nvidia-smi
gpustat
```