### Instalace homer-js na RPi 

Aktuálně halda poznámek, musím vyzkoušet na čisté RPi, co z toho je potřeba. (David)

```
Install node-js (http://weworkweplay.com/play/raspberry-pi-nodejs/):

wget http://node-arm.herokuapp.com/node_latest_armhf.deb 
sudo dpkg -i node_latest_armhf.deb

Install nvm (https://github.com/creationix/nvm/blob/master/README.markdown):

sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash

Install last node-js version:

nvm install 4 # version 4.x.x supported now!

Set current node-js version to all users (root) (https://www.digitalocean.com/community/tutorials/how-to-install-node-js-with-nvm-node-version-manager-on-a-vps#-installing-nodejs-on-a-vps):

n=$(which node);n=${n%/bin/node}; chmod -R 755 $n/bin/*; sudo cp -r $n/{bin,lib,share} /usr/local

Install gcc/g++ 4.8 (https://github.com/fivdi/onoff/wiki/Node.js-v4-and-native-addons):

sudo apt-get update
sudo apt-get install gcc-4.8 g++-4.8

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 20
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50

Install latest node-gyp:

sudo npm install -g node-gyp
sudo node-gyp rebuild

Install homer-js:
sudo npm install git+ssh://git@git.byzance.cz/homer/homer-js#develop -g --unsafe-perm
```