Install Node.js & npm Completely
Step 1: Remove Node.js & npm
```shell
sudo apt-get remove --purge nodejs npm

```
Step 2: Remove Node/NPM folders
```shell
sudo rm -rf /usr/local/lib/node_modules
sudo rm -rf ~/.npm
sudo rm -rf ~/.node-gyp
sudo rm -rf ~/.nvm
sudo rm -rf ~/.cache
sudo rm -rf /usr/local/bin/node
sudo rm -rf /usr/local/bin/npm
```
You can confirm it's gone:
```bash
node -v
npm -v

```
Reinstall Node.js (Latest LTS with npm)
Install via NodeSource (Recommended)
```shell
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

```
Then check versions:
```bash
node -v
npm -v

```
Install via `nvm` (More Flexible)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

```
Then restart terminal or run:
```bash
source ~/.bashrc

```
Install Node LTS:
```bash
nvm install --lts
nvm use --lts
```
