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
**解决**:

 1. 更改读写权限：`sudo chown -R $(whoami) /usr/local`
 2. `brew link --overwrite node`
 
```
localhost:~ v$ node -v
v8.9.1
localhost:~ v$ npm -v
5.5.1
```

参考: [https://github.com/Homebrew/brew/issues/1714](https://github.com/Homebrew/brew/issues/1714)

### react-native 0.50.1 不能 debug
releace 模式正常，debug 出现下边报错。

![debug](https://github.com/Guodadada/react-native-bug-collection/blob/master/Resources/debug.jpeg)

**解决**

  1. react-native-git-upgrade to react-native0.50.3
  2. 上面一步并没有解决问题，但是不排除可能解决部分问题。
  3. 重装了 Chrome ，clean , run-ios, 成功跑起啦。

  
参考: [https://github.com/facebook/react-native/issues/16674](https://github.com/facebook/react-native/issues/16674)