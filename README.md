# Portal FIETO
## Federação das Indústrias do Estado de Tocantins

[FIETO][fieto] is built on Hugo.


Project info
------------

- Official website: <http://fieto.com.br/>
- Code repository: <https://github.com/flowercloud-io/fieto>

Getting Started
---------------

- [Install VirtualBox][download-virtualbox]
- [Install Vagrant][download-vagrant]

Installation
------------

    $ vagrant plugin install vagrant-vbguest
    $ vagrant plugin install vagrant-hostmanager

Running
-------

    $ vagrant up
    $ vagrant ssh
    $ cd ~/fieto
    $ hugo server --theme=hugo-theme-fieto --buildDrafts

Provisioning
------------

    $ vagrant provision


[download-vagrant]: https://www.vagrantup.com/downloads.html
[download-virtualbox]: https://www.virtualbox.org/wiki/Downloads
[fieto]: http://fieto.com.br
