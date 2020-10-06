# Unity IOS support

## Apple Developer

苹果开发者分为：个人开发者，公司，企业（needs DUNS）



## APP ID

app的唯一编号



## Profile

project file 包含app ID/开发者证书/硬件 Device

可以在开发者中心配置完成后添加到xcode，也可以在xcode上连接开发者中心生成

真机调试时需要在其中添加UDID

是进行真机调试和上架的必备之物



# 开发流程

1】取得开发者账户（如果是公司或者企业开发者，需要获得公司授权）

2】在账户中创建开发者证书，APP ID，如果包含推送，则要创建推送证书

3】在Profile中绑定所有证书ID，添加调试真机



# 开发者证书的创建

## 1】登陆开发者中心

点击【Certificates，identifiers & Profiles】

点击【右上角的加号】



## 2】创建证书 Select Type

### Development/ios APP Development

开发测试证书，用于进行真机调试



### Production/App Store and Hoc

发布证书，用于在appstore发布产品



### Apple Push Notification service SSL

苹果推送证书



## 3】创建证书请求  Request

证书签名请求文件

点击【continue】



## 4】获取颁发证书

1】点击【Launchpad】/【 钥匙串访问】

2】点击【证书助理】/【从证书颁发机构请求证书】

3】输入两个电子邮箱地址，用户电子邮件地址是注册的apple ID

4】输入常用名称，一般是公司名称+应用助记名

5】选择【存储到磁盘】，保存后名称应该为CertificateSigningRequest。certSigningRequest



## 5】生成证书 Generate

1】回到开发者中心页面

2】点击【Choose File】上传CSR证书



## 6】下载证书 Download

点击【Download】下载证书



# Xcode配置开发者证书

1】进入【Xcode Preference / Account】

2】点击 左下角【+号】添加开发者账户

3】点击 右下角【Manager Certificate】

4】在弹出对话框点击+，添加iOS Development与Mac Development证书

5】选择【project/Targets/General/**signing**/Team】设置签名信息

























