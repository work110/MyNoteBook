# Unity Notebook

unity关联修复

vs2017可以直接调试

vs2019需要在调试按钮中进行调试

# Time

## Time.detalTime	

每一帧间隔的更新时间，注意在time.scale=0的时候不可用



## Time.fixedDetalTime 

准确的描述时停间隔



## AutoRunAndRun 定时循环执行

```c#
float SetTime; //设定循环间隔
float CurrentTime;

void Update(){
    if(CurrentTime > SetTime){
        //重置计时器
        CurrentTime = 0;
        
        Debug.log("我来搞个大新闻");
    }  
    CurrentTime +=Time.fixedDeltaTime;
    
}
```



## AutoClose 定时自毁

```c#
float SetTime；
float CurrentTime；
    
void OnEnable(){
    //开启
}

void OnDisable(){
    CurrentTime = SetTime; //重置时间
  
    Debug.log("我要爆炸了 ");
}

void Update(){
    //计时器倒数刷新
    CurrentTime -= Time.fixedDeltaTime;
    if(CurrentShowTime <= 0){
     	this.gameobject.SetActive(false);   
    }
}
```



# 延迟执行

## Invoke(方法字符串，延迟执行的时间)

注意注意这个方法只能够在没有时停的方式下使用



# UI

## Onclick Event

为按钮绑定事件

```c#
using UnityEngine.UI;

void Start(){
    Button btn = this.GetComponent<Button>();
    btn.onClick.AddListener(OnClick);
}

void OnClick(){
    //这里是点击事件
}
```





# Animator 动画状态机

## 常用函数

```c#
Animator FSM;

//获取动画状态机
FSM = this.GetComponent<Animator>(); 

//获取当前状态机是否是某个状态
FSM.GetCurrentAnimatorStateInfo(0).IsName("状态名称1");

//设置状态机自带值
FSM.SetInteger("整型数值名",值);
FSM.SetBool("布尔数值名",值);

```





























