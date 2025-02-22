---
title: 应用图标
desc: (@quasar/app-vite) 如何用 Capacitor 管理 Quasar 混合移动应用程序的图标。
---

就图标而言，Capacitor 是所有构建目标中最复杂的一个，因为不仅需要将图标放在特定的文件夹中，还需要在两个平台（Android、iOS）的配置文件中注册它们。

如果发现有一个文件是新的或丢失的，请 [打开这个 issue](https://github.com/quasarframework/quasar/issues).

<img src="https://cdn.quasar.dev/img/iconfactory.png" style="float:right;max-width:15%;min-width:240px;padding-top:40px" />

## 图标精灵命令行界面

::: tip 提示
强烈建议使用 [图标精灵命令行界面](/icongenie/introduction)，因为它消耗一个图标源，并自动克隆、缩放、最小化，并把图标放在适当的目录中。当需要时，它还会告诉你需要在 /index.html 文件中添加哪些标签。
:::

用图标精灵命令行界面快速启动必要的图像。有关完整的选项清单，请访问 [图标精灵命令行界面](/icongenie/command-list) 的命令清单页面。

```bash
$ icongenie generate -m capacitor -i /path/to/source/icon.png [-b /path/to/background.png]
```

根据将使用的打包器（electron-packager 或 electron-builder），请看他们关于如何勾选图标的文档。

## 使用说明

除非你使用图标精灵应用扩展，否则这些是需要替换的文件：

```
.
├── android
│   └── app
│       └── src
│           └── main
│               └── res
│                   ├── drawable
│                   │   └── splash.png
│                   ├── drawable-land-hdpi
│                   │   └── splash.png
│                   ├── drawable-land-mdpi
│                   │   └── splash.png
│                   ├── drawable-land-xhdpi
│                   │   └── splash.png
│                   ├── drawable-land-xxhdpi
│                   │   └── splash.png
│                   ├── drawable-land-xxxhdpi
│                   │   └── splash.png
│                   ├── drawable-port-hdpi
│                   │   └── splash.png
│                   ├── drawable-port-mdpi
│                   │   └── splash.png
│                   ├── drawable-port-xhdpi
│                   │   └── splash.png
│                   ├── drawable-port-xxhdpi
│                   │   └── splash.png
│                   ├── drawable-port-xxxhdpi
│                   │   └── splash.png
│                   ├── mipmap-hdpi
│                   │   ├── ic_launcher.png
│                   │   ├── ic_launcher_foreground.png
│                   │   └── ic_launcher_round.png
│                   ├── mipmap-mdpi
│                   │   ├── ic_launcher.png
│                   │   ├── ic_launcher_foreground.png
│                   │   └── ic_launcher_round.png
│                   ├── mipmap-xhdpi
│                   │   ├── ic_launcher.png
│                   │   ├── ic_launcher_foreground.png
│                   │   └── ic_launcher_round.png
│                   ├── mipmap-xxhdpi
│                   │   ├── ic_launcher.png
│                   │   ├── ic_launcher_foreground.png
│                   │   └── ic_launcher_round.png
│                   └── mipmap-xxxhdpi
│                       ├── ic_launcher.png
│                       ├── ic_launcher_foreground.png
│                       └── ic_launcher_round.png
└── ios
    └── App
        └── App
            └── Assets.xcassets
                ├── AppIcon.appiconset
                │   ├── AppIcon-20x20@1x.png
                │   ├── AppIcon-20x20@2x-1.png
                │   ├── AppIcon-20x20@2x.png
                │   ├── AppIcon-20x20@3x.png
                │   ├── AppIcon-29x29@1x.png
                │   ├── AppIcon-29x29@2x-1.png
                │   ├── AppIcon-29x29@2x.png
                │   ├── AppIcon-29x29@3x.png
                │   ├── AppIcon-40x40@1x.png
                │   ├── AppIcon-40x40@2x-1.png
                │   ├── AppIcon-40x40@2x.png
                │   ├── AppIcon-40x40@3x.png
                │   ├── AppIcon-512@2x.png
                │   ├── AppIcon-60x60@2x.png
                │   ├── AppIcon-60x60@3x.png
                │   ├── AppIcon-76x76@1x.png
                │   ├── AppIcon-76x76@2x.png
                │   └── AppIcon-83.5x83.5@2x.png
                └── Splash.imageset
                    ├── splash-2732x2732-1.png
                    ├── splash-2732x2732-2.png
                    └── splash-2732x2732.png
```
