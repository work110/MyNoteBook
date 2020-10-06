# [C] SDK dev Note



# 腾讯游戏语言sdk

## 1】准备工作

【1】腾讯云，注册，在sdk中心中搜索unity，点击游戏多媒体语言

【2】下载unity demo 

【3】在云市场购买8块钱5000分钟的语言聊天

【4】记录下 【appid】与【authykey】

## 

## 2】ios-unity项目更改

### 1】system Sample Rate =48000

在ios项目中，更改 【projectsetting-》audio-》system Sample Rate =48000】



### 2】IosProjectScrip修改

在IosProjectScript中，注释以下代码

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using System.Runtime.InteropServices;
using UnityEngine;
using AOT;


public class IosProjectScript : UnityEngine.MonoBehaviour {  
	[UnityEditor.Callbacks.PostProcessBuild(999)]  
	public  static void OnPostprocessBuild (UnityEditor.BuildTarget BuildTarget, string path){  
		if (BuildTarget == UnityEditor.BuildTarget.iOS) {  
			UnityEngine.Debug.Log (path);  
			
			{  
				string projPath = UnityEditorAV.iOS.Xcode.PBXProject.GetPBXProjectPath (path);  
				UnityEditorAV.iOS.Xcode.PBXProject proj = new UnityEditorAV.iOS.Xcode.PBXProject ();  
				
				proj.ReadFromString (System.IO.File.ReadAllText (projPath));  
				string target = proj.TargetGuidByName (UnityEditorAV.iOS.Xcode.PBXProject.GetUnityTargetName ());  
				
                //这个是省事添加库的，可以参考
				proj.AddFrameworkToProject (target, "CoreTelephony.framework", false);
				proj.AddFrameworkToProject (target, "OpenAL.framework", false);
				proj.AddFrameworkToProject (target, "libc++.tbd", false);
				proj.AddFrameworkToProject (target, "libz.tbd", false);
				proj.AddFrameworkToProject (target, "libresolv.9.tbd", false);
				proj.AddFrameworkToProject (target, "libsqlite3.0.tbd", false);
				proj.AddFrameworkToProject (target, "AssetsLibrary.framework", false);

                //注释掉各种打包的强制命名
                
				//proj.AddExternalLibraryDependency(target,"libsqlite3.0.tbd",proj.AddFile())
				//proj.AddExternalProjectDependency("/Users/tobinchen/Documents/Project/OpenSDK_feiche/platform_client/avsdk_pack/avsdk_pack.xcodeproj","sss",UnityEditor.iOS.Xcode.PBXSourceTree.Absolute);

				proj.SetBuildProperty (target, "ENABLE_BITCODE", "NO");
				
				//proj.SetBuildProperty (target, "CODE_SIGN_IDENTITY", "iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd");//"iPhone Distribution: Tencent Technology (Shanghai) Co., Ltd (FN2V63AD2J)" "iPhone Developer: qifeng chen (FYD54BA7D7)"
				//proj.SetBuildProperty (target, "CODE_SIGN_IDENTITY[sdk=iphoneos*]", "iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd");
				//proj.SetBuildProperty (target, "PROVISIONING_PROFILE","16722ba2-6fd1-45ef-a009-f94b20bc0d4f");
				//proj.SetBuildProperty (target, "PROVISIONING_PROFILE_SPECIFIER","16722ba2-6fd1-45ef-a009-f94b20bc0d4f");
				proj.SetBuildProperty (target, "CODE_SIGN_STYLE","Manual");
				//proj.SetBuildProperty (target,"PRODUCT_BUNDLE_IDENTIFIER", "com.tencent.GMEDemoUnity");
				//proj.SetBuildProperty (target,"DEVELOPMENT_TEAM", "");
				//proj.SetBuildProperty (target,"PRODUCT_NAME", "GMEDemo");
				//proj.SetBuildProperty (target, "PRODUCT_BUNDLE_IDENTIFIER", "com.tencent.qavsdkdemo");
				
				proj.AddBuildProperty(target,"OTHER_LDFLAGS","-ObjC");
				proj.AddBuildProperty(target,"GCC_PREPROCESSOR_DEFINITIONS","__declspec(noreturn)=__attribute__((noreturn))");
			
	

				System.IO.File.WriteAllText (projPath, proj.WriteToString ());
			}  
			
			{  
				string plistPath = path + "/Info.plist";
				UnityEditorAV.iOS.Xcode.PlistDocument plist = new UnityEditorAV.iOS.Xcode.PlistDocument ();  
				plist.ReadFromString (System.IO.File.ReadAllText (plistPath));  
				UnityEditorAV.iOS.Xcode.PlistElementDict rootDict = plist.root;
				
				rootDict.SetString ("NSMicrophoneUsageDescription", "QAVSDKDemo");
				rootDict.SetBoolean ("UIFileSharingEnabled", true);
				
				// UnityEditorAV.iOS.Xcode.PlistElementDict NSAppTransportSecurity = rootDict.CreateDict("NSAppTransportSecurity"); 
				// NSAppTransportSecurity.SetBoolean("NSAllowsArbitraryLoads", true);
				
				UnityEditorAV.iOS.Xcode.PlistElementArray CFBundleDocumentTypes = rootDict.CreateArray("CFBundleDocumentTypes"); // just for test
				CFBundleDocumentTypes.AddDict().CreateArray("LSItemContentTypes").AddString("public.content");
				
				rootDict.SetString ("NSCameraUsageDescription", "QAVSDKDemo");
				System.IO.File.WriteAllText (plistPath, plist.WriteToString ());  
 			}
		}
	}  
}
```



### 3】Automatically Sign=yes

在【player settings】中修改【 Automatically Sign 】为yes



### 4】修改包名

### 5】导入profile

### 6】导出xcode项目

### 7】导入xcode工程

### 8】bitcode=NO

修改【project-》unity-iphone-》build setting 】中搜索【bitcode】设置为NO



### 9】添加静态库libresolv.tbd

在【Targets-》UnityFrameWork-》build Phases -》Link Sinary With Libraries】中添加静态库【libresolv.tbd】



### 10】 automatically manage signing =yes

修改【Targets-》Unity-iPhone-》signing & Capabilities -》 勾选 automatically manage signing 】



### 11】team选择开发者

12】出包



