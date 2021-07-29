# Ansible极简指南

> 测试环境：
> 宿主机：macOS 11.5.7
> 受控机：Fedora 33

### 确认受控机环境

安装并开启了ssh服务，且允许root用户登录

参考：<https://lzwang.ltd/post/linux_ssh/>

### 在宿主机和受控机之间建立免密登录

```shell
ssh-copy-id root@10.211.55.7
```

### 新增Ansible受控机配置

```shell
sudo mkdir /etc/ansible
sudo vim /etc/ansible/hosts
```

编辑如下内容：

```shell
[pd]
10.211.55.7 ansible_ssh_user=root
```

### 测试ansible连接

```shell
ansible all -m ping
```

### 修改Ansible配置文件

```shell
vim ~/.ansible.cfg
```

配置参考：<https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg>

### 执行简单的Playbook

```yaml
# linux_install_vim.yaml
- hosts: pd
  tasks:
    - name: install vim
      yum: name=vim state=present
```

```shell
ansible-playbook linux_install_vim.yaml
```

