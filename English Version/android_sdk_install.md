# Android SDK Install



## Gradle
> Gradle 是 Google 官方推荐的构建 Android 程序的工具，使用 Android Studio 进行开发的时候，它会自动在新建的项目中包含一个自带的命令行工具 gradlew。我们推荐开发者使用这个自带的命令行工具，这是因为 Gradle 存在版本兼容的问题，很多开发者即使正确配置了 Gradle 脚本，但由于使用了最新版本或不兼容的 Gradle 版本而仍然无法成功加载依赖包。

Googel suggests use Gradle.

## Android Studio

> 使用 Android Studio 创建一个新的项目的时候，它的目录结构如下：

When you create a new project with Android Studio, the structure of the project is:

```
.
├── app                 // 应用源代码 // code of app
    ├── ...
    ├── build.gradle    // 应用 Gradle 构建脚本 // Gradle of app
    ├── ...
├── build.gradle        // 项目 Gradle 构建脚本 // Gradle of project
├── YOUR-APP-NAME.iml   // YOUR-APP-NAME 为你的应用名称 // YOUR-APP-NAME is name of your app
├── gradle
└── settings.gradle
+
```

> 首先打开根目录下的 build.gradle 进行如下标准配置：

First open the build.gradle file under root directory and add:

```
buildscript {
    repositories {
        jcenter()
        //这里是 LeanCloud 的包仓库
        maven {
            url "http://mvn.leancloud.cn/nexus/content/repositories/releases"
        }

    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.0.0'
    }
}

allprojects {
    repositories {
        jcenter()
        //这里是 LeanCloud 的包仓库
        maven {
            url "http://mvn.leancloud.cn/nexus/content/repositories/releases"
        }
    }
}
```

> 然后打开 app 目录下的 build.gradle 进行如下配置：

Then open the build.gradle file under app directory and add:

```
android {
    //为了解决部分第三方库重复打包了META-INF的问题
    packagingOptions{
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE.txt'
    }
    lintOptions {
        abortOnError false
    }
}

dependencies {
    compile ('com.android.support:support-v4:21.0.3')

    //avoscloud-sdk 为 LeanCloud基础包
    compile ('cn.leancloud.android:avoscloud-sdk:v3.+')

    //avoscloud-push 为推送与实时聊天需要的包
    compile ('cn.leancloud.android:avoscloud-push:v3.+@aar'){transitive = true}

    //avoscloud-statistics 为 LeanCloud 统计包
    compile ('cn.leancloud.android:avoscloud-statistics:v3.+')

    //avoscloud-feedback 为 LeanCloud 用户反馈包
    compile ('cn.leancloud.android:avoscloud-feedback:v3.+@aar')

    //avoscloud-sns 为 LeanCloud 第三方登录包
    compile ('cn.leancloud.android:avoscloud-sns:v3.+@aar')
    compile ('cn.leancloud.android:qq-sdk:1.6.1-leancloud')

    //avoscloud-search 为 LeanCloud 应用内搜索包
    compile ('cn.leancloud.android:avoscloud-search:v3.+@aar')
}
```

> 我们已经提供了官方的 maven 仓库，推荐大家使用。

We provide [maven](http://mvn.leancloud.cn/nexus/).
