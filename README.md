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

### npm install 安装过慢，仅临时切换源

```
npm install --registry=http://registry.npm.taobao.org

```



### Android 下 /node_modules/react-native/third-party/glog-0.3.4/test-driver'. Couldn't follow symbolic link.

根据 github 上的回复，只要遇到 Couldn't follow symbolic link. 就刪除发生错误的文件夹即可。


### FlatList Item 的属性和 State 有关联时，State 改变，FlatList 不更新界面问题

解决：给FlatList指定extraData={this.state}属性


### 使用svg格式图片防止失真
可以生成 ttf 格式的网站 [https://icomoon.io/app/#/select]()

步骤：
 
- 向网站导入 SVG 格式的图片
- 选中所有上传的 SVG
- Generate Font
- 下载
- 讲 ttf 和 selection.json 替换到项目中（Android 和 iOS）

### react-native run-ios fails: ENOENT no such file or directory, uv_chdir


[https://github.com/facebook/react-native/issues/11293]()
For me I just do a react-native upgrade then react-native run-ios and it works


### ActivityIndicator 

ActivityIndicator 使用必须设置高度，否则显示不出来

```

 <ActivityIndicator animating={moreLoading}
                    style={{marginRight: px2dp(10), height: 15}}
                    size={'small'}/>

```


### NSPhotoLibraryAddUsageDescription 报错

**iOS 11 新特性**

在 `info.plist` 中添加 `Privacy - Photo Library Additions Usage Description`，并说明理由

"Privacy - Photo Library Additions Usage Description”

Specifies the reason for your app to get write-only access to the user’s photo library. See NSPhotoLibraryAddUsageDescription for details.

iOS 11 and later

参考: [https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html]()


### 保存服务器的图片到相册

由于API：`saveToCameraRoll(tag, type?)` 在 `Android` 上 `tag` 必须是本地的 `URI`

**iOS 可以通过`RN`提供的 `CameraRoll` 实现**

1. 先把原生的库添加到项目中，`Xcode` 中添加 `RCTCameraRoll.xcodeproj`，添加 `lib`
2. 下边代码实现保存到相册。

```

CameraRoll
	.saveToCameraRoll(imgURL, 'photo')
	.then((res) => {
                		console.log('res ===> ', res);
                		toastShort('保存成功');
                })

```


**Andorid**

通过 `react-native-fetch-blob`，下载到本地，再通过 `CameraRoll` 写入相册

```
RNFetchBlob
	.config({path: PictureDir + '/userThumbnails/user.png'})
	.fetch('GET', imgURL, {
		'Cache-Control': 'no-store'
		})
	.then((res) => {
		CameraRoll.saveToCameraRoll('file://' + res.path(), 'photo').then((res) => {
			console.log('res ===> ', res);
			toastShort('保存成功');
		})
	});
```


### git 打分支

工具是 `WebStorm`

- 创建一个分支：右下角点击`git`，`NewBranch`
- 在新分支中写代码，不影响别的分支。
- 切换分支：CheckOut


### 画虚线

```
borderStyle: 'dashed'

```