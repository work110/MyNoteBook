# 【C】AssetBundle



## 用法

将prefab，图片，音乐，材质球等等放在服务器上，当加载的时候进行使用

简称AB包



## 热更新

C#不是脚本语言，不能进行热更新

热更新需要使用lua的方式进行

但是C#的跨平台性较好，非常稳定

# Prefab的设置

## 1】场景

建立三个3D物体，建立一个材质球，将三个3D物体设置为材质球的物体



### 【对齐摄影机】

选择摄影机，选择Align with View 则可以将摄像机设置到scene面板角度



## 2】AssetBundle设置

建立prefabs文件夹，建立mat文件夹

在【Inspector】面板右下角AssetBundle 设置文件名，后缀id



# 创建AB tool

## 1】编写AB包脚本

创建【editor】文件夹，editor脚本是放在编辑器中运行的

```c#
using UnityEditor; //编辑下运行使用的脚本
using System.IO; 

public class MyTools:Editor{  //编辑下运行的脚本
  
  [MenuItem(“Tools/CreateAssetBundle”)] //这是在菜单中设置一个子菜单
  Static Void CreateAssetBundle(){
    	UnityEngine.Debug.Log("AB tools Starts");
    	string ABPath = "AB"; //相对路径，用来存放ab包
    
    	if(Directory,Exists(path)){
        Directory.CreatDirectory();
      }
    
    	//打包管线，建立ab包，在其下设置64位平台等
    	BuildPipeline.BuildAssetBundles(ABPath,BuildAssetBundleOptions.None,BuildTatget.StandalioneWindows64);
     
  }
}
```



## 2】点击工具栏进行运行

可以在设置的文件夹中查看其生成的文件



## 【Manifast】

生成的ab包文件后面还有manifast，在manifast中可以看到相关的内容，包括他的路径和依赖



## 【AB打包参数设置】

BuildAssetBundleOptions.None //使用默认lz4格式压缩，下载后直接加载

BuildAssetBundleOptions.UncompressedAssetBundle //不进行数据压缩

BuildAssetBundleOptions.UncompressedAssetBundle //使用lz4进行数据压缩，加载时才进行解压，但是会卡

BuildAssetBundleOptions.CollectDependencies //包含所有依赖关系

BuildAssetBundleOptions.CompleteAssets //强制包含整个资源



## 【打包细节】

如果ABC三个物体都使用了1号材质球，那么如果1号材质球没有设置为AB包

那么ABC三个物体都会包含材质球进行打包，材质会非常的庞大

# LoadFromMemory

```c#
using UnityEngine;
using System.Collections;//携程
using System.IO; 

public class LoadAssetBundle: MonoBehaviour{
  
  void Start(){
    ABFromMemory();
  }
   
  //文件方式加载
  IEnumerator ABFromFiel(){
    
    //【1】加载路径数组
    string path= @"";//注意路径前加@关闭转义字符
    byte[] bytes = File.ReadAllBytes(path);
    
    //【2】ab包加载到内存，需要一个二进制数组
    AssetBundle AB = AssetBundle.loadFromMemory(bytes); // 同步加载
    
    //【3】从内存ab包中读取gameobject
    Gameobject go =AssetBundle.LoadAsset("Cube")as GameObject; //cube的名字可以从manifast中读取
    
    //【4】实例化
    Gamoobject.Instatiate(go);
    
    yield return null; //携程返回null
  }
 
}
```

## 【材质球丢失】

如果材质球丢失的话可以放在AB包中拿到

# LoadFromFile


```c#
using UnityEngine;
using System.Collections;//携程
using System.IO; 

public class LoadAssetBundle: MonoBehaviour{
  
  void Start(){
    AB();
  }
   
  //加载
  IEnumerator AB(){
    
    //【1】加载路径
    string path= @"";//注意路径前加@关闭转义字符
    
    //【2】ab包加载到内存，需要一个二进制数组
    AssetBundle AB = AssetBundle.loadFromFile(path); // 同步加载
    
    //【3】从内存ab包中读取gameobject
    Gameobject go =AssetBundle.LoadAsset("Cube")as GameObject; //cube的名字可以从manifast中读取
    
    //【4】实例化
    Gamoobject.Instatiate(go);
    
    yield return null; //携程返回null
  }
 
}
```



# LoadAllAssets

把所有资源放到一个assets中，然后进行加载


```c#
using UnityEngine;
using System.Collections;//携程
using System.IO; 

public class LoadAssetBundle: MonoBehaviour{
  
  void Start(){
    AB();
  }
   
  //加载
  IEnumerator AB(){
    
    //【1】加载路径
    string path= @"";//注意路径前加@关闭转义字符
    
    //【2】读文件加载
    AssetBundle AB = AssetBundle.loadFromFile(path); // 同步加载
    
    //【3】读取所有asset
    object[]  lists = asset.LoadAllAsset()as GameObject; 
    
    //【4】实例化
    foreach(var go in lists){
      Debug.log(((GameObject)go).name);//输出名字
      Gamoobject.Instatiate((GameObject)go));
    }
    
    
    yield return null; //携程返回null
  }
 
}
```











# 从网络中加载AB包

```c#
using UnityEngine;
using System.Collections;//携程

public class LoadAssetBundle: MonoBehaviour{
  
  void Start(){
    ABFromMemory();
  }
   
  //内存方式加载
  IEnumerator ABFromMemory(){
    
    //加载路径数组
    string path="";//绝对路径
    byte[] bytes = File.ReadAllBytes(path);
    
    //ab包加载到内存，需要一个二进制数组
    AssetBundle AB = AssetBundle.loadFromMemory(bytes); // 同步加载
    
    //从内存ab包中读取gameobject
    Gameobject go =AssetBundle.LoadAsset("Cube")as GameObject; //cube的名字可以从manifast中读取
    Gamoobject.Instatiate(go);
    
    yield return null; //携程返回null
  }
 
}
```




















