# conda配置pytorch

**环境：** win11 + conda 4.13.0

- 查看cuda版本，我的是11.6
  ```bash
  nvidia-smi
  ```
  
- 更换清华源，加快下载速度
  ```bash
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/
  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  
  conda config --set show_channel_urls yes
  ```

- 创建pytorch环境
  ```bash
  conda create -n pytorch python=3.9
  ```
  根据要求输入y即可，然后执行
  ```bash
  activate pytorch
  ```
  
- 去官网 https://pytorch.org/get-started/locally/ 根据CUDA选择相应的版本，然后官方给出提示可通过运行 `conda install pytorch torchvision torchaudio cudatoolkit=11.6 -c pytorch -c conda-forge` 安装
  
  由于要使用清华源加速，把原命令里面带有 `-c` 的都删去，执行下面的命令。
  ```bash
  conda install pytorch torchvision torchaudio cudatoolkit=11.6
  ```
  
  **在根据提示输入y之后，安装过程中可能会如下错误：**
  ```bash
  WARNING conda.gateways.disk.delete:unlink_or_rename_to_trash(143): 
  Could not remove or rename D:\Anaconda3\pkgs\pytorch-1.11.0-py3.7_cuda11.3_cudnn8_0\Lib\site-packages\torch\lib\cudnn_ops_train64_8.dll.  
  Please remove this file manually (you may need to reboot to free file handles)
  ```
  手动删除对应路径上的文件，退出去后再打开Anaconda prompt，进入pytorch环境，再次执行安装命令。
  
- 运行后可能还会报错，如下所示：
  ```bash
  CondaVerificationError: The package for pytorch located at D:\Anaconda3\pkgs\pytorch-1.11.0-py3.7_cuda11.3_cudnn8_0
  appears to be corrupted. The path 'Lib/site-packages/torch/include/ATen/ops/zeros_compositeimplicitautograd_dispatch.h'
  specified in the package manifest cannot be found.
  ```
  如果有上述错误，则输入下述代码
  ```bash
  conda clean --all
  ```
  然后退出去再执行一次安装命令，就可以安装成功了。
