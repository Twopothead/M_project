[TOC]
# M-Project 

Copyright (C) 2017 Frank Curie (邱日)

------------------------



# 开发环境

## VScode
- download : https://code.visualstudio.com/docs?start=true

- install :  

  ```shell
  sudo dpkg -i code_1.21.1-1521038896_amd64.deb code_1.21.1-1521038896_amd64.deb
  ```

- run: 

  - https://blog.csdn.net/FernChen/article/details/52259692

  - ```python
    #encoding:utf-8
    print "hello"
    ```

  - terminal: python hello.py

  - ctrl+B:

    ```javascript
    {
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
        "version": "2.0.0",
        "tasks": [
            {
                "label": "echo",
                "type": "shell",
                "command": "python",
                "args": [
                    "${file}"
                ],
                "group": {
                    "kind": "build",
                    "isDefault": true
                }
            }
        ]
    }
    ```

- theme (optional)

  - Extensions: One Dark Pro



# 文档

- 中文文档　https://www.gitbook.com/book/wizardforcel/keras-cn/details　(download PDF)

- You can also get docs(zh) using **mkdocs**:

  - ```shell
    sudo apt-get install mkdocs
    git clone git://github.com/keras-team/keras-docs-zh
    cd keras-docs-zh
    mkdocs build
    # then you will get 'site' directory here,they are html pages.

    ```

  ​

# Anaconda

- ```shell
  sudo chmod 777 Anaconda2-4.3.0-Linux-x86_64.sh
  ./Anaconda2-4.3.0-Linux-x86_64.sh
  ```

- ```sh
  Anaconda2 will now be installed into this location:
  /home/curie/anaconda2

    - Press ENTER to confirm the location
    - Press CTRL-C to abort the installation
    - Or specify a different location below

  [/home/curie/anaconda2] >>> 
  PREFIX=/home/curie/anaconda2
  Do you wish the installer to prepend the Anaconda2 install location
  to PATH in your /home/curie/.bashrc ? [yes|no]
  [no] >>> yes
  Prepending PATH=/home/curie/anaconda2/bin to PATH in /home/curie/.bashrc
  A backup will be made to: /home/curie/.bashrc-anaconda2.bak
  For this change to become active, you have to open a new terminal.
  Thank you for installing Anaconda2!

  ```

- ```sh
  /home/curie/.bashrc
  # added by Anaconda2 4.3.0 installer
  export PATH="/home/curie/anaconda2/bin:$PATH"
  ```

- ```shell
  conda install tensorflow
  conda install keras
  ```

  - ​

    ```shell
    sudo conda install ipython
    ```

  - ```sh
    sudo apt-get install aptitude
    sudo aptitude install python-dev 
    ```
    ​

    ```
    Do you wish the installer to prepend the Anaconda3 install location
    to PATH in your /home/curie/.bashrc ? [yes|no]
    [no] >>> 
    You may wish to edit your .bashrc to prepend the Anaconda3 install location to PATH:

    export PATH=/home/curie/anaconda3/bin:$PATH

    Thank you for installing Anaconda3!

    ```

    ​


# 问题解决

## pip

### pip目录的属主不是sudo的root用户

- http://blog.sina.com.cn/s/blog_a046022d0102w2ux.html

- ```shell
  sudo chown root /home/curie/.cache/pip
  sudo chown root /home/curie/.cache/http
  ```


### 安装好keras后但发现没有

- 用pip3安装后都安装到了/usr/local/lib/python3.6/dist-packages里了 [路径问题](https://blog.csdn.net/tsinghuahui/article/details/76223354)

- 问题是pip向系统自带的python安装而不向anaconda安装

  - ```
    ubuntu直接安装anaconda是不能直接使用pip 的，因为pip install需要sudo权限，而sudo pip是系统自带的python的pip 
    这两个是不一样的
    ```

  - https://blog.csdn.net/zl87758539/article/details/73823641

- 权限不够

  An error occurred while uninstalling package 'defaults::conda-4.4.10-py36_0'.

  - ```shell
    sudo chown -R curie:curie /home/curie/anaconda3
    #再删去系统中除了anaconda3之外的conda,只留这个anaconda3里面的conda
    ```



## 问题解决日志

### 2018.3.23

因为重装系统,环境需要重装,但遇到问题,解决如下.

- 系统的pip和anaconda里的pip还不是一个,用sudo pip 安装到了系统python下,因此应当conda install

- conda 又遇到问题,在于conda也不止一个,whereis conda,删去系统里的conda,只留anaconda里的conda

- 这样conda只剩一个,然而又遇到权限问题

  - ```
    #遇到的错误:
    ERROR conda.core.link:_execute(481): An error occurred while uninstalling package 'defaults::conda-4.4.10-py36_0'.
    ```

  - ```shell
    ##先解决权限问题
    sudo chown -R curie:curie /home/curie/anaconda3
    ##再更新conda
    conda update -n base conda
    conda install keras
    ```