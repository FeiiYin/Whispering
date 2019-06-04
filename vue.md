## Vue 安装

安装node.js，npm

***安装python2环境***  

`node-sass` required	

修改`python.exe` 为 `python2.exe`

`npm install --registry=https://registry.npm.taobao.org`

`npm run dev`

注册源`npm config set registry http://registry.npm.taobao.org`	



#### <font color=#FF0000>error</font> 

`Node Sass could not find a binding for your current environment: Windows 64-bit with Node.js 10.x`

#### solution

`npm rebuild node-sass`

`npm update`

#### <font color=#FF0000>error</font>	

`gyp verb could not find “msbuild.exe” in PATH - finding location in registry`

`gyp ERR! stack Can’t find “msbuild.exe”. Do you have Microsoft Visual Studio C++ 2008+ installed?`

#### solution

`npm config set sass-binary-site http://npm.taobao.org/mirrors/node-sass`

`npm install node-sass`

#### run

`npm run dev`

#### <font color=#FF0000>error</font>	

`Error: spawn xxxx ENOENT`

#### solution

path环境变量配置不当，导致无法找到指定的程序，如`Error: spawn cmd.exe ENOENT`，出现该问题的原因是因为没有将`%SystemRoot%\system32`加入path变量中



:-(  



## 框架

element <https://element.eleme.cn/2.0/#/zh-CN/component/tree>

框架模板

[https://panjiachen.github.io/vue-element-admin-site/zh/guide/#%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84](https://panjiachen.github.io/vue-element-admin-site/zh/guide/#目录结构)

download

<https://github.com/PanJiaChen/vue-element-admin>



## Problem

vue 里不能多余空行与空格