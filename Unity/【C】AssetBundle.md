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



# Editor中创建AB tool

1】创建【editor】文件夹，editor脚本是放在编辑器中运行的

```c#
using UnityEditor;

public class MyTools:Editor{
  
  [MenuItem(“Tools/CreateAssetBundle”)]
  Static Void CreateAssetBundle(){
    	UnityEngine.Debug.Log("this is AB tools");
    
  }
}
```















