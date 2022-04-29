### EXP2

#### 1.New Project（选择Basic Activity）

#### 2 FirstFragment

##### 	2.1添加button

​		添加两个button，并将现有的三个botton分别将id改为TOAST,COUNT,RANDOM.

​		调整布局、修改UI，布局如下：

![button](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp2/ScreenShots/button.png)

​		代码如下：

```xml
<Button
    android:id="@+id/random_button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginEnd="24dp"
    android:background="@color/buttonBackground"


    android:text="@string/next"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/textview_first" />

<Button
    android:id="@+id/toast_button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="24dp"
    android:background="@color/buttonBackground"
    android:text="@string/toast_button_text"


    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/textview_first" />

<Button
    android:id="@+id/count_button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/count_button_text"
    android:background="@color/buttonBackground"

    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toStartOf="@+id/random_button"
    app:layout_constraintStart_toEndOf="@+id/toast_button"
    app:layout_constraintTop_toBottomOf="@+id/textview_first"
    />
```

​		

##### 	2.2文本

​		将TextView的id属性改为textview_first，代码如下：

```xml
<TextView
    android:id="@+id/textview_first"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/hello_first_fragment"
    android:textColor="#FFFFFF"
    android:textSize="72sp"
    app:layout_constraintVertical_bias="0.3"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```



##### 	2.3FirstFragment中添加代码完成应用程序交互

###### 		2.3.1TOAST按钮添加一个toast消息

​			onCreateView中添加以下代码：

```kotlin
view.findViewById<Button>(R.id.toast_button).setOnClickListener {
    // create a Toast with some text, to appear for a short time
    val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
    // show the Toast
    myToast.show()
}
```

###### 		2.3.2randomButton

​			onCreateView中添加以下代码：

```kotlin
view.findViewById<Button>(R.id.random_button).setOnClickListener {
//            random(view)
//            findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
            val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
            val currentCount = showCountTextView.text.toString().toInt()
            val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
            findNavController().navigate(action)

        }
```

###### 		2.3.3Count

​			onCreateView中添加以下代码：

```kotlin
view.findViewById<Button>(R.id.count_button).setOnClickListener {
    countMe(view)
}
```

```
private fun countMe(view: View) {
    // Get the text view
    val showCountTextView = view.findViewById<TextView>(R.id.textview_first)

    // Get the value of the text view.
    val countString = showCountTextView.text.toString()

    // Convert value to a number and increment it
    var count = countString.toInt()
    count++

    // Display the new value in the text view.
    showCountTextView.text = count.toString()


}
```

*第一界面完成结果如下*

![frement_first](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp2/ScreenShots/frement_first.png)

#### 3 SecondFragment

##### 	3.1添加TextView用来显示随机数

​		设新TextView的id为textview_random

​		代码如下：

```xml
<TextView
    android:id="@+id/textview_random"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="R"
    android:textColor="#FFFFFF"
    android:textSize="72sp"
    android:textStyle="bold"
    app:layout_constraintBottom_toTopOf="@+id/button_second"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/textview_header"
    app:layout_constraintVertical_bias="0.45" />
```

##### 	3.2更新显示界面文本的TextView(Textview_second)

```xml
<TextView
    android:id="@+id/textview_header"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginStart="24dp"
    android:layout_marginTop="24dp"
    android:layout_marginEnd="24dp"
    android:textColor="@color/colorPrimaryDark"
    android:textSize="24sp"
    android:text="@string/random_heading"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="1.0"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.122" />
```

*布局如下*

![frement_second](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp2/ScreenShots/frement_second.png)

##### 	3.3启用SafeArgs

​		buildscript中加入

```
ext.nav_version = "2.3.0-alpha01"
```

​		dependencies中加入

```
classpath "androidx.navigation:navigation-safe-args-gradle-plugin:$nav_version"
```

​		plugins中加入

```
id 'androidx.navigation.safeargs.kotlin'
```

##### 	3.4 FirstFragment添加代码，向SecondFragment发数据

​		将onViewCreated()方法中的代码改为：

```kotlin
val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
val currentCount = showCountTextView.text.toString().toInt()
val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
findNavController().navigate(action)
```

##### 	3.5 SecondFragment添加代码

​		导入navArgs包

```kotlin
import androidx.navigation.fragment.navArgs
```

​		onViewCreated()代码之前添加

```kotlin
val args: SecondFragmentArgs by navArgs()
```

​		onViewCreated()方法中添加

```kotlin
val count = args.myArg
val countText = getString(R.string.random_heading, count)
view.findViewById<TextView>(R.id.textview_header).text = countText
```

```kotlin
val random = java.util.Random()
var randomNumber = 0
if (count > 0) {
    randomNumber = random.nextInt(count + 1)
}
view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()
```

#### 4 运行结果

![result](https://github.com/ChenyangLiuu/Software-project-development-practice/blob/main/exp2/ScreenShots/result.png)

