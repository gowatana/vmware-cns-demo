# VMware CNS デモむけの Oracle Linux 7 / CentOS 7 設定

下記の投稿むけです。  
vSphere / vSAN 6.7 U3 と Kubernetes で VMware Cloud Native Storage を試してみる。
<https://communities.vmware.com/people/gowatana/blog/2019/08/28/k8s-csi-vsan>


Ansible の準備。

```
## Oracle Linux 7
# yum install -y --enablerepo=ol7_addons ansible git

## CentOS 7
# yum install -y ansible git
```

Ansible を実行するサーバに、Playbook などをダウンロード。

```
$ git clone http://
```

設定対象の指定と確認。

```
$ cp inventory/hosts.template inventory/hosts
$ vi inventory/hosts
$ ssh-copy-id root@xxx.xxx.xxx.xxx
$ ansible all -m ping
```

OS 設定と、docker / kubeadm　などのインストール。  
設定内容によっては、最後に OS が自動リブートされることあり。

```
$ ansible-playbook setup_os.yml
```

Kubernetes Master / Worker にするサーバにデモむけファイルを配置。

```
$ ansible-playbook copy_config_files.yml
```

# 参考
About Getting Started with VMware Cloud Native Storage  
<https://docs.vmware.com/en/VMware-vSphere/6.7/Cloud-Native-Storage/GUID-51D308C7-ECFE-4C04-AD56-64B6E00A6548.html>


EOF
