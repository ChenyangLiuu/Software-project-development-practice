### EXP3

##### 导入项目

​	git clone https://github.com/hoitab/TFLClassify.git

##### 运行初始代码

​	出现SDK版本过低的问题

![29](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/29.png)

​	解决方法：将SDK版本升级到32

![32](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/32.png)

​	真机调试

​		1.鸿蒙系统设置中连续点击7次*版本号*，并且开启USB调试

![develop](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/develop.jpg)

​		2.选择物理机作为运行设备

![myphone](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/myphone.png)

​	成功运行（此时还不具备识别花卉的功能）

![1](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/1.jpg)

##### 向项目中添加TensorFlow Lite

​	1.选择"start"模块

​	2.右键“start”模块，或者选择File，然后New>Other>TensorFlow Lite Model

![addmodel](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/addmodel.png)

​	3.选择已经下载的自定义的训练模型。本教程模型训练任务以后完成，这里选择finish模块中ml文件下的FlowerModel.tflite

![path](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/path.png)

​	4.点击Finish后自动生成摘要

![info](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/info.png)

##### 补完代码中的TODO项

​	1.定位“start”模块**MainActivity.kt**文件的TODO 1，添加初始化训练模型的代码

```kotlin
private val flowerModel = FlowerModel.newInstance(ctx)
```

​	2.定位TODO 2，添加以下代码，使摄像头的输入`ImageProxy`转化为`Bitmap`对象，并进一步转化为`TensorImage` 对象

```kotlin
val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
```

​	3.定位TODO 3，添加以下代码，对图像进行处理并生成结果

```kotlin
val outputs = flowerModel.process(tfImage)
    .probabilityAsCategoryList.apply {
        sortByDescending { it.score } // Sort with highest confidence first
    }.take(MAX_RESULT_DISPLAY) // take the top results
```

​	4.定位TODO 4，添加以下代码，将识别的结果加入数据对象`Recognition` 中，包含`label`和`score`两个元素。后续将用于`RecyclerView`的数据显示

```kotlin
for (output in outputs) {
    items.add(Recognition(output.label, output.score))
}
```

​	5.注释原来虚假识别结果的代码

```kotlin
//            for (i in 0 until MAX_RESULT_DISPLAY){
//                items.add(Recognition("Fake label $i", Random.nextFloat()))
//            }
```

##### 重新运行APP

​	识别成功

<table frame=void>	<!--使用table标签，且frame=void消除外边框-->
	<tr>		   <!--<tr>一行的内容<\tr>，<td>一个格子的内容<\td>-->
    <td><center><img src="https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/rose.jpg"		
                     alt="找不到图片，可能是网络原因"
                     height="520"/></center></td>	<!--<center>标签将图片居中-->
    <td><center><img src="https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp3/ScreenShots/sunflower.jpg"
                     alt="找不到图片，可能是网络原因"
                     height="520"/></center></td>
    </tr>
</table>
