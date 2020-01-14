# vagrant

https://app.vagrantup.com/ubuntu/boxes/trusty64

`
% vagrant box add "ubuntu/trusty64"
`
![image](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant_add_box.png)

`
% vagrant box list
ubuntu/trusty64 (virtualbox, 20190514.0.0)
`

但是這樣會倒到 ubuntu 的雲端去, 取得下載網址
https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/20190514.0.0/providers/virtualbox.box

下載到 local 來

在 local 建一個檔案 metadata.json
`
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
`
vagrant box list | cut -f 1 -d ' ' | xargs -L 1 vagrant box remove -f

![image](https://github.com/Charles-Hsu/vagrant/blob/master/add_local_vagrant_box.png)
`
vagrant init ubuntu/trusty64
`
![image](https://github.com/Charles-Hsu/vagrant/blob/master/vagrant_init.png)
