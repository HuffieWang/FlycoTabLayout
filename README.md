# FlycoTabLayout
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-FlycoTabLayout-green.svg?style=true)](https://android-arsenal.com/details/1/2756)

## 声明

由于大家对于AndroidX的呼声越来越高，而原作者又长期不更新。
本人fork了此仓库([relish-wang/FlycoTabLayout](https://github.com/relish-wang/FlycoTabLayout))并在jcenter上发布了支持AndroidX的新版本(v3.0.0)。
```groovy
implementation 'com.flyco.tablayout:FlycoTabLayout_Lib:3.0.0'
```
但由于我无法发布到中央仓库(与原作者的依赖坐标重复; 没有修改坐标也是为了尊重原作), 所以如果你需要使用支持AndroidX的新版本(v3.0.0)还需要在你工程根目录下的`build.gradle`的`allprojects`节点下的`repositories`节点中添加这行代码):
```groovy
maven { url "https://dl.bintray.com/relish-wang/maven/" }
```
像这样:
```groovy
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.4.2'
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://dl.bintray.com/relish-wang/maven/" } // 添加这行
    }
}
```
这样你就完成了对FlycoTabLayout_Lib的AndroidX改造。


一个Android TabLayout库,目前有3个TabLayout

* SlidingTabLayout:参照[PagerSlidingTabStrip](https://github.com/jpardogo/PagerSlidingTabStrip)进行大量修改.
    * 新增部分属性
    * 新增支持多种Indicator显示器
    * 新增支持未读消息显示
    * 新增方法for懒癌患者
    
    ```java
        /** 关联ViewPager,用于不想在ViewPager适配器中设置titles数据的情况 */
        public void setViewPager(ViewPager vp, String[] titles)
        
        /** 关联ViewPager,用于连适配器都不想自己实例化的情况 */
        public void setViewPager(ViewPager vp, String[] titles, FragmentActivity fa, ArrayList<Fragment> fragments) 
    ```

* CommonTabLayout:不同于SlidingTabLayout对ViewPager依赖,它是一个不依赖ViewPager可以与其他控件自由搭配使用的TabLayout.
    * 支持多种Indicator显示器,以及Indicator动画
    * 支持未读消息显示
    * 支持Icon以及Icon位置
    * 新增方法for懒癌患者
    
    ```java
        /** 关联数据支持同时切换fragments */
        public void setTabData(ArrayList<CustomTabEntity> tabEntitys, FragmentManager fm, int containerViewId, ArrayList<Fragment> fragments)
    ```

* SegmentTabLayout

## Demo
![](./preview_1.gif)

![](./preview_2.gif)

![](./preview_3.gif)


>## Change Log

 > v3.0.0(2019-07-27)
 >
 >    - 支持AndroidX(minSdkVersion升级到14)

 > v2.0.0(2016-03-01)
   - 删除了对FlycoRoundView库的依赖
   - 新增方法getIconView和getTitleView(为了某些情况需要动态更新icon之类的)

 > v2.0.2(2016-04-23)
 >
 >    - 删除了对NineOldAnimation库依赖(仅支持3.0+)

## Gradle

```groovy
dependencies{
    compile 'com.android.support:support-v4:23.1.1'
    compile 'com.nineoldandroids:library:2.4.0'
    compile 'com.flyco.roundview:FlycoRoundView_Lib:1.1.2@aar'
    compile 'com.flyco.tablayout:FlycoTabLayout_Lib:1.5.0@aar'
}

After v2.0.0(support 2.2+)
dependencies{
    compile 'com.android.support:support-v4:23.1.1'
    compile 'com.nineoldandroids:library:2.4.0'
    compile 'com.flyco.tablayout:FlycoTabLayout_Lib:2.0.0@aar'
}

After v2.0.2(support 3.0+)
dependencies{
    compile 'com.android.support:support-v4:23.1.1'
    compile 'com.flyco.tablayout:FlycoTabLayout_Lib:2.1.2@aar'
}

After v3.0.0(support 4.0+ and use AndroidX)
dependencies{
    implementation 'androidx.appcompat:appcompat:1.0.2'
    implementation 'com.flyco.tablayout:FlycoTabLayout_Lib:3.0.0'
}
```
**使用v3.0.0注意事项:**
由于jcenter规定我不能发布和原作者相同路径的仓库。(这是我遇到的警告:`Failed to send a message: Path is already exist in JCenter.`)
所以如果你的项目不得不使用AndroidX, 同时又依赖着FlycoTabLayout_Lib, 那么在升级到3.0.0的时候需要将下面这行代码加
入到你的工程根目录下的`build.gradle`的`allprojects`节点下的`repositories`节点中(注意不是app/build.gradle):
```groovy
maven { url "https://dl.bintray.com/relish-wang/maven/" }
```
像这样:
```groovy
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.4.2'
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://dl.bintray.com/relish-wang/maven/" } // 添加这行
    }
}
```

## Attributes

|name|format|description|
|:---:|:---:|:---:|
| tl_indicator_color | color |设置显示器颜色
| tl_indicator_height | dimension |设置显示器高度
| tl_indicator_width | dimension |设置显示器固定宽度
| tl_indicator_margin_left | dimension |设置显示器margin,当indicator_width大于0,无效
| tl_indicator_margin_top | dimension |设置显示器margin,当indicator_width大于0,无效
| tl_indicator_margin_right | dimension |设置显示器margin,当indicator_width大于0,无效
| tl_indicator_margin_bottom | dimension |设置显示器margin,当indicator_width大于0,无效 
| tl_indicator_corner_radius | dimension |设置显示器圆角弧度
| tl_indicator_gravity | enum |设置显示器上方(TOP)还是下方(BOTTOM),只对常规显示器有用
| tl_indicator_style | enum |设置显示器为常规(NORMAL)或三角形(TRIANGLE)或背景色块(BLOCK)
| tl_underline_color | color |设置下划线颜色
| tl_underline_height | dimension |设置下划线高度
| tl_underline_gravity | enum |设置下划线上方(TOP)还是下方(BOTTOM)
| tl_divider_color | color |设置分割线颜色
| tl_divider_width | dimension |设置分割线宽度
| tl_divider_padding |dimension| 设置分割线的paddingTop和paddingBottom
| tl_tab_padding |dimension| 设置tab的paddingLeft和paddingRight
| tl_tab_space_equal |boolean| 设置tab大小等分
| tl_tab_width |dimension| 设置tab固定大小
| tl_textsize |dimension| 设置字体大小
| tl_textSelectColor |color| 设置字体选中颜色
| tl_textUnselectColor |color| 设置字体未选中颜色
| tl_textBold |boolean| 设置字体加粗
| tl_iconWidth |dimension| 设置icon宽度(仅支持CommonTabLayout)
| tl_iconHeight |dimension|设置icon高度(仅支持CommonTabLayout)
| tl_iconVisible |boolean| 设置icon是否可见(仅支持CommonTabLayout)
| tl_iconGravity |enum| 设置icon显示位置,对应Gravity中常量值,左上右下(仅支持CommonTabLayout)
| tl_iconMargin |dimension| 设置icon与文字间距(仅支持CommonTabLayout)
| tl_indicator_anim_enable |boolean| 设置显示器支持动画(only for CommonTabLayout)
| tl_indicator_anim_duration |integer| 设置显示器动画时间(only for CommonTabLayout)
| tl_indicator_bounce_enable |boolean| 设置显示器支持动画回弹效果(only for CommonTabLayout)
| tl_indicator_width_equal_title |boolean| 设置显示器与标题一样长(only for SlidingTabLayout)

## Dependence
*   [NineOldAndroids](https://github.com/JakeWharton/NineOldAndroids)
*   [FlycoRoundView](https://github.com/H07000223/FlycoRoundView)

## Thanks
*   [PagerSlidingTabStrip](https://github.com/jpardogo/PagerSlidingTabStrip)
