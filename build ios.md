# vue项目使用Hbuilder打包苹果IOS-App详细教程
## 打包苹果IOSapp首先需要准备以下几项东西：
1. 已经编写好的vue项目。
2. 电脑上安装好Hbuilder。
3. 准备苹果手机一台。
4. 注册苹果开发者账号（个人、企业均可）。
   
### 一、申请苹果账号
&nbsp;&nbsp;&nbsp;&nbsp;如果还没注册过苹果账号，先通过以下链接注册一个，如果有苹果账号了请直接看第二步！
https://appleid.apple.com/account?localang=zh_CN

### 二、申请ios 证书（p12）和描述文件
#### 准备环境
* 必需要有苹果开发者账号，并且加入了 “iOS Developer Program”
* Mac OS 10.9以上系统（如果已经申请p12证书则不需要）
1. 登录 [iOS Dev Center](https://developer.apple.com/devcenter/ios/index.action)
2. 登录成功后在页面左侧选择 “Certificates,IDs & Profiles” 进入证书管理页面：![](https://ask.dcloud.net.cn/uploads/article/20191112/13b79b72faf48a3217cde91d4bc81f96.png)
3. 选择页面的 “Identifiers" 可查看到已申请的所有 App 应用标识，点击页面上的加号来创建一个新的应用标识，选择标识类型为 “App IDs”，然后点击 “Continue”：![](https://ask.dcloud.net.cn/uploads/article/20191112/ae9c05f4b59605cecf83cfd3b3aea5c5.png)

4. 平台选择 “iOS，tvOS，watchOS”，Bundle ID 选择 “Explicit”，在 Description 中填写描述，然后填写 Bundle ID，Bundle ID 要保持唯一性，建议填写反域名加应用标识的格式 如：“io.dcloud.hellouniapp”， 然后点击 “Continue”
注意：在 HBuilderX 中 App 提交云端打包时界面上的 AppID 栏填写的就是这个 Bundle ID![](https://ask.dcloud.net.cn/uploads/article/20191112/fd7f98a5285afd17c186bcd1a0dddcb1.png)
5. 接下来需要选择应用需要使用的服务（如需要使用到消息推送功能，则选择“Push Notifications”），然后点击 “Continue”
注意：如果App用不到的服务一定不要勾选，以免响应审核![](https://ask.dcloud.net.cn/uploads/article/20191112/35b2007afc9e32009b6472d8358c6d2a.png)
6. 在“Spltlight Search”中搜索“钥匙串”并打开 “钥匙串访问” 工具，将证书请求文件保存到指定路径下，后面申请开发(Development)证书和发布(Production)证书时需要用到：![](https://ask.dcloud.net.cn/uploads/article/20191112/1294a8472389b0fec9d9ef341c1f9be9.png)![](https://ask.dcloud.net.cn/uploads/article/20191112/890875c122389dcaec03850081acc65e.png)
7. 申请开发(Development)证书，在证书管理页面选择 “Certificates" 可查看到已申请的所有证书（TYPE：Development 为开发证书，Distribution为发布证书），点击页面的加号来创建一个新的证书：
![](https://ask.dcloud.net.cn/uploads/article/20191112/74051174ffd099862d2d28d5657d9e18.png)![](https://ask.dcloud.net.cn/uploads/article/20191112/e07ae5f61ee512c71574e0c2a910d8b6.png)
在证书管理页面选择 “Certificates" 可查看到已申请的所有证书（TYPE：Development 为开发证书，Distribution为发布证书），点击页面的加号来创建一个新的证书：
![](https://ask.dcloud.net.cn/uploads/article/20191112/7b2e445496991680483c66eef460fb7d.png)
生成证书后选择 “Download” 将证书下到本地 (ios_development.cer)：![](https://ask.dcloud.net.cn/uploads/article/20191112/36cdfc238a95e7409a0f05cfed68acff.png)
双击保存到本地的 ios_development.cer 文件，会自动打开 “钥匙串访问” 工具说明导入证书成功，可以在证书列表中看到刚刚导入的证书，接下来需要导出 .p12 证书文件，选中导入的证书，右键选择 “导出...”：![](https://ask.dcloud.net.cn/uploads/article/20191112/bb24badaf2becb672559bc289494833f.png)
至此，我们已经完成了开发证书的制作（得到了 xxx.p12 证书文件），接下来，继续生成开发阶段所需的描述文件，在生成描述文件之前，需要先添加调试设备（iPhone 、iPad）
8. 申请开发 (Development) 描述文件  
在证书管理页面选择 “Profiles”，可查看到已申请的所有描述文件，点击页面上的加号来添加一个新的描述文件：![](https://ask.dcloud.net.cn/uploads/article/20191112/0e5ff848e1e83facf20455f4705d0aa4.png)
在 “Development” 栏下选中 “iOS App Development”，点击“Continue”按钮：![](https://ask.dcloud.net.cn/uploads/article/20191112/e0dfd711b73264cc18cd551359f40a7e.png)
这里要选择之前创建的 “App ID” (这里是“io.dcloud.hellouniapp”)，点击“Continue”：![](https://ask.dcloud.net.cn/uploads/article/20191112/10aacf646f0d14cf26751eba620ce4c2.png)
接下来选择需要绑定的证书，这里建议直接勾选 “Select All”，点击“Continue”：
![](https://ask.dcloud.net.cn/uploads/article/20191112/b3b64702a3cf4857c97047c7a3f54c92.png)
选择授权调试设备，这里建议直接勾选 “Select All”，点击 “Continue”：![](https://ask.dcloud.net.cn/uploads/article/20191112/80777452245069ebae852fc811b0956d.png)
输入描述文件的名称（如“HelloUniAppProfile”）, 点击 “Generate” 生成描述文件：![](https://ask.dcloud.net.cn/uploads/article/20191112/47aecc44fa2367e99876b05b93dc4feb.png)
至此，我们已经得到了开发证书（.p12）及对应的描述文件（.mobileprovision）

## 三、打包ipa
1. 将vue项目运行npm run build 指令，进行项目编译。
编译好之后生成的dist文件夹内的所有东西，复制到新启动的Hbuilder的项目中，替换掉原来的文件夹，保留unpackage文件夹和manifest.json文件。
![](https://upload-images.jianshu.io/upload_images/10881829-6cd758ea358cf98f.png?imageMogr2%2Fauto-orient%2Fstrip%7CimageView2%2F2%2Fw%2F1200%2Fformat%2Fwebp)![](https://upload-images.jianshu.io/upload_images/10881829-3e7b545817f4e26c.png?imageMogr2%2Fauto-orient%2Fstrip%7CimageView2%2F2%2Fw%2F1200%2Fformat%2Fwebp)
2. 选择iOS打包，支持的设备类型（可以选择支持iPhone和支持ipad），选择使用苹果证书  
AppID：跟申请证书描述.mobileprovision时选择的要一致（又称套装id，appid，BundleID，应用id，包名）  
profile文件：选择上传配置文件.mobileprovision  
私钥证书：上传.p12文件  
私钥密码：输入创建p12设置的密码。  
3. 打包成功后，下载保存ipa，这个ipa包就能安装到手机测试了。![](https://upload-images.jianshu.io/upload_images/10881829-f8a0c477337fb02f.png?imageMogr2%2Fauto-orient%2Fstrip%7CimageView2%2F2%2Fw%2F1200%2Fformat%2Fwebp)

## 四、用iTunes安装测试
