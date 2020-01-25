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
    
這時會在目錄裡產生一個 Vagrantfile 的設定檔

##### 開始使用 vagrnat box

     $ cd ubuntu_trusty64
     $ vagrant up
     $ vagrant ssh
     
![image](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant-up.png)

#### 改壞了 /etc/networking/interface 檔

設定要取得外部的網路 IP 位址, 直接去更改 /etc/networking/interface 檔, 結果無法執行 vagrant up. google 結果似乎是要直接更改 Vagranfile 裡頭的 networking 的設定值, 但目前的 vm 已經裝好了 GoBelieveIO 的 chat server, 不太想要重來一次. 發現, 原來可以由 VirtualBox 直接執行 Vagrant VM, 這時會提示你 username 和 password, 直接給 vagrant/vagrant 就可以進去 VM 把 interfaces 改回來.

- 不確定怎麼設定後會跑出 vboxnet0 這個 ifconfig 檔

![](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant-vboxnet0.png)

在 Vangrantbox 檔案裡頭加入這個

    config.vm.network "private_network", ip: "192.168.50.100"
    
然後重新載入 Vangrantfile

    $ vagrant reload
    $ vagrant ssh
    
    $ ifconfig
    
![](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant-ifconfig-50.100.png)

