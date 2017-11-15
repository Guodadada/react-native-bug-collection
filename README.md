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


### react-native run-ios 报 `-bash: react-native: command not found`

***解决：***

1. 是否安装 Yarn, React Native 的命令行工具（react-native-cli），未安装终端运行下边代码：

	```
	npm install -g yarn react-native-cli
	```
2. 安装完测试 `react-native -v` 是否打印版本。
3. 不打印进行下边操作：

	```
	localhost:~ v$ npm list -g | head -n 1
	
	// 得到一个路径 比如：/home/baptiste/.linuxbrew/lib
	// 用 bin 替换 路径末尾的 lib
	// 添加全局变量：export PATH="/home/baptiste/.linuxbrew/bin:$PATH"
	// 重启终端
	// 测试 react-native -v
	
	localhost:~ v$ react-native -v
react-native-cli: 2.0.1
react-native: n/a - not inside a React Native project directory
	
	```
	
参考：[https://stackoverflow.com/questions/33282545/bash-react-native-command-not-found](https://stackoverflow.com/questions/33282545/bash-react-native-command-not-found)


### react-native run-ios 报错：`xcrun: error: unable to find utility "instruments", not a developer tool or in PATH`

***解决：***在 终端执行如下命令 sudo xcode-select -s /Applications/Xcode.app/Contents/Developer/


### react-native 给图片设置圆角

```
image: {
       redius: 15
       overflow: 'hidden'
    },

```

### bash gradle command not found && gradle: Permission denied


参考：[http://blog.csdn.net/u013424496/article/details/52684213](http://blog.csdn.net/u013424496/article/details/52684213)

参考：[https://stackoverflow.com/questions/17668265/gradlew-permission-denied](https://stackoverflow.com/questions/17668265/gradlew-permission-denied)


### Could not install the app on the device, read the error above for details.Make sure you have an Android emulator running or a device connected and have set up your Android development environment:

解决：终端执行下边的命令

```
chmod 755 android/gradlew

/**
 * 1.文件所有者可读可写可执行
 * 2.与文件所有者同属一个用户组的其他用户可读可执行 
 * 3.其它用户组可读可执行
 */

```
