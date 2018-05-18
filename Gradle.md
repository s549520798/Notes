---
date : 2018-5-18 
title : android gradle 配置
---

#### 生成自定义apk文件
因为android studio 3.0之后output.outputFile 变成只读，所以使用之前的配置会报错
1. AS3.0版本之前的配置
```
    android{
        ......
        // 打包后应用名称
        applicationVariants.all { variant ->
            variant.outputs.each { output ->
                def outputFile = output.outputFile
                def fileName
                if (outputFile != null && outputFile.name.endsWith('.apk')) {
                    if (variant.buildType.name.equals('release')) {
                        fileName = "hlct_release${defaultConfig.versionName}.${getTime()}.apk"
                    } else if (variant.buildType.name.equals('debug')) {
                        fileName = "hlct_debug${defaultConfig.versionName}.${getTime()}.apk"
                    }
                    output.outputFile = new File(outputFile.parent, fileName)
                }
            }
        }
    }
```
2.AS3.0版本之后的配置
```
    android{
        ......
        // 打包后应用名称
        applicationVariants.all { variant ->
            variant.outputs.all { output ->
                def outputFile = output.outputFile
                def fileName
                if (outputFile != null && outputFile.name.endsWith('.apk')) {
                    if (variant.buildType.name == 'release') {
                        fileName = "name_release${defaultConfig.versionName}.${getTime()}.apk"
                    } else if (variant.buildType.name == 'debug') {
                        fileName = "name_debug${defaultConfig.versionName}.${getTime()}.apk"
                    }
                    outputFileName = fileName
                }
            }
        }
    }
```