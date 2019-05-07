
to run vagrant, you need;

|              vagrant               |               git-scm                |     virtualbox     |      composer       |
| :--------------------------------- | -----------------------------------: | :----------------- | ------------------: |
| [x] vagrantup.com                  |                      [x] git-scm.com | [x] virtualbox.org | [x] getcomposer.org |
| vagrant  box add laravel/homestead |                                      |                    |                     |
| choose virtualbox                  | cd C: git clone ../laravel/homestead |                    |                     |
| cd vagrant/box                     | edit homestead.yml                   |                    |  create ssh key     |
|~/Homestead,vagrant up --provision  | vagrant ssh (to login the VM)        |  apt-get update    |                     |

- [x] composer global require laravel/installer
- [ ] git clone url into the parent folder
- [ ] !! init.bat // to create homestead.yaml
- [ ] laravel new project --force (폴더가 존재하기 때문에)
- [ ] ssh-keygen -t rsa -b 4096 -C "onofftony@gmail.com"
- [ ] vagrant up --provision

to delete files;
rm -rf filename

## laravel setup

after setting the path in environment of path, run;
composer global require "laravel/installer"

cd into the home directory (cd laravel-apps/)
laravel new laravelwidnows

### how to set PATH in pc environment

echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bash_profile

or
echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

before that, run;
cp path/.bashrc.swp  ./.bashrc
<!-- ls -la ~/ | more
vi ~/.bashrc -->
ssh-keygen -t rsa -b 4096 -C "eozz21@gmail.com"  // ~/.ssh folder

C:\Windows\System32\Drivers\etc\hosts
then,
# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
192.168.10.10 homestead.app
alias hosts="sudo nano /etc/hosts"
alias yml="nano ~/.homestead/Homestead.yml"

## yml edit

provider: virtualbox
authorize: ~/.ssh/id_rsa.pub

keys:
    - ~/.ssh/id_rsa

folders:
    - map: C:\laravel-apps
      to: /home/vagrant/Code

sites:
    - map: laravelwindows.app
      to: /home/vagrant/Code/laravlewindows/public

databases:
    - homestead


## how to set up hosts

C:/windows/system32/dirvers/etc .. hosts // open with adminstrator  to brackets

C:\Windows\System32\Drivers\etc\hosts
then,
# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
192.168.10.10 laravelwindows.app

## how to setup
yml - map
host - 192..... demo.app
vagrant up --provision
composer create-project laravel/laravel demo
vagrant ssh
laravel new demo

