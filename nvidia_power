#!/bin/bash
# check for driver
command -v nvidia-smi &> /dev/null || { echo >&2 "nvidia driver is not installed you will need to install this from community applications ... exiting."; exit 1; }
echo "Nvidia drivers are installed"
echo
echo "I can see these Nvidia gpus in your server"
echo
nvidia-smi --list-gpus 
echo
echo "-------------------------------------------------------------"
# set persistence mode for gpus ( When persistence mode is enabled the NVIDIA driver remains loaded even when no active processes, 
# stops modules being unloaded therefore stops settings changing when modules are reloaded
nvidia-smi --persistence-mode=1
#query power state
gpu_pstate=$(nvidia-smi --query-gpu="pstate" --format=csv,noheader);
#query running processes by pid using gpu
gpupid=$(nvidia-smi --query-compute-apps="pid" --format=csv,noheader);
#check if pstate is zero and no processes are running by checking if any pid is in string
if [ "$gpu_pstate" == "P0" ] && [ -z "$gpupid" ]; then
echo "No pid in string so no processes are running"
fuser -kv /dev/nvidia*
echo "Power state is"
echo "$gpu_pstate" # show what power state is
else
echo "Power state is" 
echo "$gpu_pstate" # show what power state is
fi
echo
echo "-------------------------------------------------------------"
echo
echo "Power draw is now"
# Check current power draw of GPU
nvidia-smi --query-gpu=power.draw --format=csv
exit

