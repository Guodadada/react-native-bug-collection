# react-native-bug-collection
react-native bug collection

## 环境安装

### 使用 `brew install node` 
安装完成后运行 `brew ls` 及 `node -v`

```
localhost:~ v$ brew install node
touch: /usr/local/Homebrew/.git/FETCH_HEAD: Permission denied
fatal: Unable to create '/usr/local/Homebrew/.git/index.lock': Permission denied
error: could not lock config file .git/config: Permission denied
==> Downloading https://homebrew.bintray.com/bottles/node-8.9.1.high_sierra.bott
Already downloaded: /Users/v/Library/Caches/Homebrew/node-8.9.1.high_sierra.bottle.tar.gz
==> Pouring node-8.9.1.high_sierra.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink etc/bash_completion.d/npm
/usr/local/etc/bash_completion.d is not writable.

You can try again using:
  brew link node
Warning: The post-install step did not complete successfully
You can try again using `brew postinstall node`
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/node/8.9.1: 5,012 files, 49.4MB

localhost:~ v$ brew ls
icu4c	node

localhost:~ v$ node -v
-bash: node: command not found
```
All of them are:

 1. 更改读写权限：`sudo chown -R $(whoami) /usr/local`
 2. `brew link --overwrite node`
 
```
localhost:~ v$ node -v
v8.9.1
localhost:~ v$ npm -v
5.5.1
```
