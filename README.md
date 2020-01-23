# vagrant

https://app.vagrantup.com/ubuntu/boxes/trusty64

    % vagrant box add "ubuntu/trusty64"

![image](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant_add_box.png)

    % vagrant box list
    ubuntu/trusty64 (virtualbox, 20190514.0.0)

但是這樣會倒到 ubuntu 的雲端去, 取得下載網址
    
    https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/20190514.0.0/providers/virtualbox.box

下載到 local 來, 檔名為

    trusty-server-cloudimg-amd64-vagrant-disk1.box

改個名字

    $ mv trusty-server-cloudimg-amd64-vagrant-disk1.box ubuntu_trusty-v20190514.0.0.box
    
在 local 建一個檔案 metadata-ubuntu-trusty64.json

    {
        "name": "ubuntu/trusty64",
        "versions": 
        [
            {
                "version": "v20190514.0.0",
                "providers": [
                    {
                      "name": "virtualbox",
                      "url": "ubuntu_trusty-v20190514.0.0.box"
                    }
                ]
            }
        ]
    }

##### 刪除所有的 box 的指令

    vagrant box list | cut -f 1 -d ' ' | xargs -L 1 vagrant box remove -f
    
##### 加入 box 的指令

    vagrant box add metadata-ubuntu-trusty64.json

![image](https://github.com/Charles-Hsu/vagrant/blob/master/add_local_vagrant_box.png)

##### 初始化 box 的指令

    vagrant init ubuntu/trusty64

![image](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant_init.png)
`
chia@mbp VirtualBox VMs% vagrant init ubuntu/trusty64
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
`

sftp chia@172.20.10.2

sftp> get model_for_website-20200112T081702Z-001.zip

sudo apt install unzip
unzip model_for_website-20200112T081702Z-001.zip
cd model_for_website/
python
Python 2.7.6 (default, Nov 13 2018, 12:45:42)
python svm_test_single_image.py
ImportError: No module named numpy
sudo apt-get install python-pip

$ python3
Python 3.4.3 (default, Nov 12 2018, 22:25:49)
[GCC 4.8.4] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit
Use exit() or Ctrl-D (i.e. EOF) to exit
>>> exit()
vagrant@vagrant-ubuntu-trusty-64:~/model_for_website$ python3 svm_test_single_image.py
Traceback (most recent call last):
  File "svm_test_single_image.py", line 8, in <module>
    import numpy as np
ImportError: No module named 'numpy'

$ sudo apt-get install python3-pip
$ pip3 install numpy
RuntimeError: Python version >= 3.5 required.
$ python3
Python 3.4.3 (default, Nov 12 2018, 22:25:49)

$ sudo apt-get install python3.6
$ 
![image](https://github.com/Charles-Hsu/vagrant/blob/master/pythonx.png)

$ ln -s file1 link1
$ sudo rm python3
$ sudo ln -s python3.6 python3
$ pip3 install numpy
AttributeError: module 'importlib._bootstrap' has no attribute 'SourceFileLoader'

$ python3 -m ensurepip --upgrade
/usr/bin/python3: No module named ensurepip

$ sudo apt-get install python3.6-venv
$ python3 -m ensurepip --upgrade
Could not install packages due to an EnvironmentError: [Errno 13] Permission denied: '/usr/bin/easy_install'
Consider using the `--user` option or check the permissions.

$ sudo python3 -m ensurepip --upgrade
Successfully installed pip-18.1 setuptools-40.6.2

$ python3 svm_test_single_image.py
ModuleNotFoundError: No module named 'numpy'

$ sudo apt-get install python3-pip
$ pip3 install numpy
$ sudo python3 -m pip install cython
$ pip3 install numpy





