# ShaderGraph【了解】

## shader渲染过程

### 1】**顶点渲染 VertexShader

可以进行颜色计算和光照计算



### 2】图元计算 连接三角形 ShapeAssembly



### 3】**几何渲染 GeometryShader

一般曲面细分，顶点位移处于这个阶段



### 4】三角形转化为2d像素点



### 5】**片段着色器



### 6】测试与遮照等

**为可编程阶段



## ShaderLab

是一个nvidia的编程语言，类似于C语言

其中，vert代表Vextex Shader，frag代表Fragment Shader

```

v2f vert（appdata v）{
	v2f o;
	o.vertex = unityObjectToClipPod(v.vertex);
	o.uv= TRANSFORM_TEX(v.uv,_MainTex);
	UNITY_TRANSFER_FOG(o,o.vertex);
	return o;
}

Fixed4  frag(v2f i) : SV_Target{
	//sample the texture
	fixed4 col= tex2D(_MainTex,i.uv);
	
	//apple fog
	UNITY_APPLY_FOG(i.fogCoord,col);
	return col;
}
```



## 立体几何

### Matrix Opteration

矩阵运算，用于空间变换到摄像机等



### Vector Dot

向量点乘，用于视角操作，如兰伯特光照等



### Vertor Cross

向量差乘，判断险段是否相交



### 加减乘除

一般用于RGBA颜色的运算



### 例1】

```
v2f vert (appdata v){
	v2f o;
	o.position = mul(UNITY_MATRIX_MVP,v.position);	//可以得到视口的位置
	o.texcord = v.texcoord;													//uv坐标
	return o;
}
```



### 例2】lambert光照

```
inline fixed4 UnityLambertLight(SurfaceOutput s,UnityLight light){
	fixed diff = max(0,dot(s.Normal,light.dir));
	fixed4 c;
	c.rgb = s.Albedo * light.color * diff;
	c.a = s.Alpha;
	return c;
}
```



### 例3】程序化天空盒

```
v2f vert(appdata v){
	v2f o;
	o.position = mul(UNITY_MATRIX_MVP,v.position);
	o.texcoord = v.textcoord;
	return o;
}

fixed4 frag(v2f i): COLOR{
	half d = dot (normalize(i.textcoord),_UpVector)*0.5f+0.5f;
	rerurn lerp(_Color1,_Color2,pow(d,_Exponent))*_Intensity; 

}
```



# Shader Graph 123

建议使用多个显示器



## Master node 光照模型



### Unlit Master

无光照模型

只从贴图来进行渲染



### PBR Master

物理光照模型，多用于主机，效果较好



## Sample Texture 2D 贴图采样





例1】 基本的PBRshader

​										PBR

sample texture2d ——》albedo

sample texture2d ——〉Normal



## Shadergraph 添加灯光信息

shadergraph没有灯光信息，这是一个缺点

自己编写【Custom Function】

```
input 
list is empty

output
direction  vector3		//灯光方向
color			 vector1		//灯光颜色

type		String
Name		LightDirection
Body		#if SHADERGRAPH_PREVIEW
							direction = half3(0.5,0.5,0);
							Color=1;
				#else
							Light light = GetMainLight();
							Direction = light.direction;
							Color = light.color;
				#endif
```





## Custom node（Sub Graph）自定义库

【可以自己封装】

























