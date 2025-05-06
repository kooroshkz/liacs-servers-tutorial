# liacs-servers-tutorial
A brief tutorial on how to connect to LIACS servers using SSH - to be completed later in the summer

[![Watch the video](https://files.kooroshkz.com/cover.png)](https://www.youtube.com/watch?v=FVkeAoc68gQ)

## 1. Connect to LIACS

1. **Gateway**  
   ```bash
   ssh s<student-number>@ssh.liacs.nl
   ```

2. **GPU server**
   Check available servers: [https://rel.liacs.nl/labs/dslab](https://rel.liacs.nl/labs/dslab)
   Currently using **vibranium**:

   ```bash
   ssh vibranium.liacs.nl
   ```

## 2. Transfer Files

1. **Upload to gateway**

   ```bash
   scp <file-origin-address> s<student-number>@ssh.liacs.nl:~/
   ```
2. **Transfer to GPU server**

   ```bash
   scp ~/<file-name> s<student-number>@vibranium.liacs.nl:/data/<stu-number-with-s>/
   ```

## 3. Set Up Virtual Environment

### Using `venv`

```bash
python3 -m venv nc_venv
source nc_venv/bin/activate
pip install \
  torchvision==0.21.0 \
  torch==2.6.0 \
  notebook==7.3.3 \
  ipykernel==6.29.5
```

### Using Conda (if you hit version errors)

```bash
conda create -y -p ./nc_venv python=3.9
conda activate ./nc_venv
pip install \
  torchvision==0.21.0 \
  torch==2.6.0 \
  notebook==7.3.3 \
  ipykernel==6.29.5
```

## 4. Run Jobs in Background

### With `screen`

```bash
screen -S my_session
python model.py
# Detach: Ctrl+A then D
# Reattach:
screen -r my_session
screen -list   # list sessions
```

### With `tmux`

```bash
tmux new -s my_session
python model.py
# Detach: Ctrl+B then D
# Reattach:
tmux attach -t my_session
tmux ls        # list sessions
```

## 5. Handy Server Commands

```bash
htop        # monitor CPU/memory
nvidia-smi  # GPU status
gpustat     # GPU usage summary
```
