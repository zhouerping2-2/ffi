#一：使用说明
1、将package.json文件中的 electron版本替换至4.2.5
```
"dependencies": {
    "electron": "^4.2.5"
  }
```
2、将my_ffi_node_modules文件夹下的所有模块文件复制到工程node_modules文件夹下，即可引入ffi模块：
```
const ffi = require('ffi')

let dll = new ffi.Library('../dll/myDLL.dll', {
    'add': ['double', ['double', 'double']]
})

let dllresult = dll.add(1, 9)
console.log(dllresult) // 10
```
#二：编译说明：
##1、编译环境:
nodejs版本：8.11.3
node-gyp版本：3.8.0
ffi模块：github:gavignus/node-ffi#torycl/forceset-fix
electron版本：本机的electron版本无要求，只是编译时，指定4.2.5才编译成功，所以使用时才需将工程的electron版本替换成4.2.5
##2、安装过程：
```
npm install node-gyp@3.8.0 -g
npm install ffi@gavignus/node-ffi#torycl/forceset-fix --save
```
##3、编译过程:
target = 重编译的electron指定版本
arch = 64位
dist-url = 下载地址
abi = NODE_MODULE_VERSION版本
```
cd node_modules/ref
node-gyp rebuild --target=4.2.5 -arch=x64  --dist-url=https://npm.taobao.org/mirrors/atom-shell --abi=69
cd node_modules/ffi
node-gyp rebuild --target=4.2.5 -arch=x64  --dist-url=https://npm.taobao.org/mirrors/atom-shell --abi=69
```
