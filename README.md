# <center>BigDrug和SmallDrug</center>
## 使用说明
地址：
<br>
https://github.com/NorthernBrain/BigDrug
<br>
https://github.com/NorthernBrain/SmallDrug
<br>
这一个库中封装了Android6.0之后需要动态申请的权限，你只需要调用方法就可以直接拿到权限
<br>

## 使用方法
首先需要在你的Porject中的build.gradle加入maven

```java
allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://jitpack.io" }//加入这一句
    }
}
```
是在**allprojects 下的 repositories 中**加入，别加错位置了，有一个很像的位置。

之后在你的项目中的build.gradle加入依赖(**以下依赖二选一**)


选择一：
```java
implementation 'com.github.NorthernBrain:BigDrug:3.0'
```

选择二：
```java
implementation 'com.github.NorthernBrain:SmallDrug:3.0'
```


这两条依赖区别在于，如果你选择第一条，就不需要在你项目中的清单文件中再次声明权限，直接调用GetDrug就行，选择第二个，必须在清单文件中声明一次，再调用GetDrug。


## 代码实例

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        GetDrug getDrug = new GetDrug.Applicator(this)
                .getLocation()//想要什么权限直接get相应的就可以
                .getPhone()//想要什么权限直接get相应的就可以
                .getSms()//想要什么权限直接get相应的就可以
                .heal();//最后调用heal()
    }
}
```
**在调用完你需要的权限后，最后调用heal()就可以，但是不能只调用heal，会抛出异常，如果你用的是BigDrug，此时你就不需要再清单文件中声明权限，如果是SmallDrug，你必须在清单文件中声明你需要的权限**
<br><br><br>
你也可以这样调用，这样是获取所有Android6.0后的危险权限

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        GetDrug getDrug = new GetDrug();
        getDrug.getAllPermission(this);
    }
}

```
