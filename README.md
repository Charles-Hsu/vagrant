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

    chia@mbp VirtualBox VMs% vagrant init ubuntu/trusty64
    A `Vagrantfile` has been placed in this directory. You are now
    ready to `vagrant up` your first virtual environment! Please read
    the comments in the Vagrantfile as well as documentation on
    `vagrantup.com` for more information on using Vagrant.

![image](https://github.com/Charles-Hsu/vagrant/blob/master/pythonx.png)
