# ansible# laaC
Задача 1
Опишите своими словами основные преимущества применения на практике IaaC паттернов.
Какой из принципов IaaC является основополагающим?

Идемпотентность - приведение действий к одному и томуже результату.
Приминив идемпотентность в описании структуры через код,это  означает следующее. 
Наша нифрастуктура (вирутальные хосты) будут созданы так, как их описали. Преймущество данного метода заключается в следующем:

- Данная технология позволяет нам разворачивать инфраструктуру с уже заранее заготовленнымм списком нужных нам програм и команд для выполнения на установку, либо конфигурирование.
Что существенно сокращает время на разворачивание и настройку хостов в дальнейшем.

- Сохраняется поддержки версионности, т.к. код можно хранить на github.com

- Сохраняется гибкость в конфигурировании инфраструктуры. Достаточно изменить пару нужных строчек без подключения на сами хосты.

- Код является самой актуальной документацией.

Задача 2
Чем Ansible выгодно отличается от других систем управление конфигурациями?
Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?


Ansible поддерживает Push метод
С его помошью можно - запускать плейбуки в которых прописано, что и на какой сервер (группу серверов) нужно установить и в какой последовательности. какие действия нужно выполнить.
Слабое место (настройка Windows, Централизованное управление, необходим Python)

Более надёжный метод на мой взгляд будет - Гибридный.
Гибридный - можно настройть под разные задачи по разному.
Например мы можем с помошью метода PUSH (ansible) в плейбук вписать установку chef-agent которвый работает по PULL модели. И он будет брать конфигурацию с CHEF-SERVER.
Этот подход обеспечивает быстрое разворачивание инфраструктуры и мы так же можем её легко обслуживать.


Задача 3
Установить на личный компьютер:

VirtualBox
Vagrant
Ansible
Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.

virtualbox --help && vagrant --version && ansible --version

Oracle VM VirtualBox VM Selector v6.1.32_Ubuntu
(C) 2005-2022 Oracle Corporation
All rights reserved.

No special options.

If you are looking for --startvm and related options, you need to use VirtualBoxVM.



Vagrant 2.2.14



ansible [core 2.12.2]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/niko/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/niko/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.9.7 (default, Sep 10 2021, 14:59:43) [GCC 11.2.0]
  jinja version = 2.11.3
  libyaml = True



Задача 4 (*)
Воспроизвести практическую часть лекции самостоятельно.

Создать виртуальную машину.
Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
docker ps


ТЕРМИНАЛ:

vagrant up --provision
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202206.03.0' is up to date...
==> server1.netology: There was a problem while downloading the metadata for your box
==> server1.netology: to check for updates. This is not an error, since it is usually due
==> server1.netology: to temporary network problems. This is just a warning. The problem
==> server1.netology: encountered was:
==> server1.netology: 
==> server1.netology: The requested URL returned error: 404 Not Found
==> server1.netology: 
==> server1.netology: If you want to check for box updates, verify your network connection
==> server1.netology: is valid and try again.
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...

PLAY [nodes] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [server1.netology]

TASK [Create directory for ssh-keys] *******************************************
ok: [server1.netology]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] ****************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: If you are using a module and expect the file to exist on the remote, see the remote_src option
fatal: [server1.netology]: FAILED! => {"changed": false, "msg": "Could not find or access '~/.ssh/id_rsa.pub' on the Ansible Controller.\nIf you are using a module and expect the file to exist on the remote, see the remote_src option"}
...ignoring

TASK [Checking DNS] ************************************************************
changed: [server1.netology]

TASK [Installing tools] ********************************************************
ok: [server1.netology] => (item=['git', 'curl'])

TASK [Installing docker] *******************************************************
changed: [server1.netology]

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=1   






niko@ASUS-LV50:~/vagrant/Projects/ubuntu_docker_ansible$ vagrant ssh
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-110-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed 06 Jul 2022 07:21:45 PM UTC

  System load:  0.0                Users logged in:          0
  Usage of /:   13.8% of 30.63GB   IPv4 address for docker0: 172.17.0.1
  Memory usage: 24%                IPv4 address for eth0:    10.0.2.15
  Swap usage:   0%                 IPv4 address for eth1:    192.168.56.11
  Processes:    113


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Wed Jul  6 19:17:06 2022 from 10.0.2.2
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
vagrant@server1:~$ 
