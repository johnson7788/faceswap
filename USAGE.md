# Workflow

**Before attempting any of this, please make sure you have read, understood and completed the [installation instructions](../master/INSTALL.md). If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) or the [FaceSwap Discord server](https://discord.gg/FdEwxXd) instead of the main repo.**

- [Workflow](#Workflow)
- [Introduction](#Introduction)
  - [Disclaimer](#Disclaimer)
  - [Getting Started](#Getting-Started)
- [Extract](#Extract)
  - [Gathering raw data](#Gathering-raw-data)
  - [Extracting Faces](#Extracting-Faces)
  - [General Tips](#General-Tips)
- [Training a model](#Training-a-model)
  - [General Tips](#General-Tips-1)
- [Converting a video](#Converting-a-video)
  - [General Tips](#General-Tips-2)
- [GUI](#GUI)
- [Video's](#Videos)
- [EFFMPEG](#EFFMPEG)
- [Extracting video frames with FFMPEG](#Extracting-video-frames-with-FFMPEG)
- [Generating a video](#Generating-a-video)
- [Notes](#Notes)
  
# Introduction

## Disclaimer
本指南提供了一个关于换脸过程的高层次概述。它的目的不是要深入研究每一个可用的选项，而是为使用该软件提供一个有用的入门点。还有许多选项没有被本指南所涵盖。这些选项可以通过在命令行中传递 "-h "标志（例如："python faceswap.py extract -h"）或在图形用户界面中悬停选项来找到和解释。

## Getting Started
那么，你想在图片和视频中交换面孔？等等，因为首先你得了解这个应用程序将做什么，它是如何做的，以及它目前不能做什么。

这个脚本的基本运算很简单。它训练一个机器学习模型来识别和转换基于图片的两张脸。这个机器学习模型是我们的小 "机器人"，我们要教它做实际的交换，而图片是我们用来训练它的 "训练数据"。请注意，这个机器人主要是处理人脸。其他目标可能不工作。

因此，我们的计划是这样的。我们想创造一个现实，唐纳德-特朗普在总统选举中输给了尼克-凯奇；我们有他的就职典礼视频；让我们用凯奇替换特朗普。

# Extract
## 收集原始数据
为了实现这一目标，机器人需要学习识别脸谱A（特朗普）和脸谱B（尼克-凯奇）。默认情况下，机器人不知道特朗普和尼克-凯奇是什么样子。所以我们需要给它看很多图片，让它猜测哪个是哪个。所以我们首先需要这两张脸的图片。

一个可能的来源是谷歌、DuckDuckGo或Bing图片搜索。有一些脚本可以下载大量的图片。更好的图片来源是视频（来自采访、公开演讲或电影），因为这些会捕捉到更多的自然姿势和表情。幸运的是，FaceSwap已经覆盖了你，它可以从静态图像和视频文件中提取人脸。请参阅[提取视频帧](#Extracting_video_frames)了解更多信息。

欢迎在[faceswap论坛](https://faceswap.dev/forum)中列出你的图像集，或者在这个文件中添加更多的方法。

因此，现在我们有一个充满特朗普图片/视频的文件夹和一个单独的尼克-凯奇的文件夹。让我们把它们保存在我们放置FaceSwap项目的目录中。例如：`~/faceswap/src/trump`和`~/faceswap/src/cage`。

## 提取人脸
所以这里有一个问题。我们有一吨的照片和视频，但这些都是他们在做事情或与其他人在一个环境中的照片。他们的身体在那里，他们在那里与其他人在一起...... 这是一个混乱。只有当我们拥有的数据是一致的，并且专注于我们想要交换的对象时，我们才能训练我们的机器人。这就是FaceSwap首先出现的地方。

**Command Line:**
```bash
# 从照片中提取trump人脸
python faceswap.py extract -i ~/faceswap/src/trump -o ~/faceswap/faces/trump
# 从视频中提取
python faceswap.py extract -i ~/faceswap/src/trump.mp4 -o ~/faceswap/faces/trump
# 从照片中提取凯奇的人脸
python faceswap.py extract -i ~/faceswap/src/cage -o ~/faceswap/faces/cage
# 或者从视频中提取
python faceswap.py extract -i ~/faceswap/src/cage.mp4 -o ~/faceswap/faces/cage
```

**GUI:**

从文件夹中的照片中提取Trump（右侧的文件夹图标）。
![ExtractFolder](https://i.imgur.com/H3h0k36.jpg)

To extract cage from a video file (Left hand folder icon):
![ExtractVideo](https://i.imgur.com/TK02F0u.jpg)

对于输入，我们可以指定我们的照片目录或视频文件，对于输出，我们指定我们提取的人脸将被保存在哪个文件夹。
然后，脚本将尽力识别人脸，将图像裁剪成一致的大小，并将人脸保存到输出文件夹中。一个`alignments.json`文件也将被创建并保存在你的输入文件夹中。这个文件包含了将被FaceSwap使用的每个面孔的信息。

注意：这个脚本将使抓取测试数据变得更加容易，但它并不完美。它将（错误地）检测某些照片中的多张面孔，并且不能识别该面孔是否是我们想要交换的人。因此。**在开始训练前一定要检查你的训练数据。**训练数据会影响你的模型在交换方面的表现。

## General Tips
在提取训练用的人脸时，你要为每个你希望训练的对象收集大约500到5000张人脸。这些人应该是高质量的，并包含各种角度、表情和照明条件。
你不希望从视频中提取每一帧来进行训练，因为每一帧的人脸都会非常相似。
你可以通过在GUI中的选项上悬停或通过帮助标志来查看提取的全部参数列表，即。
```bash
python faceswap.py extract -h
```
一些插件有可配置的选项。你可以在以下内容中找到配置选项。`<faceswap_folder>/config/extract.ini`。你需要至少运行一次Extract或GUI来生成这个文件。

# Training a model
好了，现在你有一个装满特朗普脸谱的文件夹和一个装满凯奇脸谱的文件夹。现在怎么办？是时候训练我们的机器人了! 这将创建一个 "模型"，包含关于什么是笼子、什么是特朗普以及如何在两者之间交换的信息。

训练进程将花费最长的时间，多长时间取决于许多因数；使用的模型，图像的数量，你的GPU等。然而，一个粗略的数字是在GPU上需要12-48小时，如果在CPU上训练则需要数周。

我们指定两个面孔所在的文件夹，以及我们将保存训练模型的地方。

**Command Line:**
```bash
python faceswap.py train -A ~/faceswap/faces/trump -B ~/faceswap/faces/cage -m ~/faceswap/trump_cage_model/
# or -p to show a preview
python faceswap.py train -A ~/faceswap/faces/trump -B ~/faceswap/faces/cage -m ~/faceswap/trump_cage_model/ -p 
```
**GUI:**

![Training](https://i.imgur.com/j8bjk4I.jpg)
一旦你运行这个命令，它就会开始使用训练数据。如果你有一个预览，那么你会看到大量的斑点出现。这些是它正在学习的面孔。它们看起来不大，但你的模型还没有学到任何东西。随着时间的推移，这些斑点会越来越多地开始类似于trump和凯奇。

你要让你的模型学习，直到你对预览中的图像感到满意。要停止训练，你可以。
- 命令行：在预览窗口或控制台中按 "回车 "键
- GUI。按 "终止 "按钮

当停止训练时，模型将被保存，进程将退出。这可能需要一点时间，所以要有耐心。模型也会每100次左右保存一次迭代。

你可以在任何时候停止和恢复训练。只要把FaceSwap指向相同的文件夹就可以继续了。

## General Tips
如果你用mask训练或使用Warp to Landmarks，你将需要为每个面孔集传入一个`alignments.json`文件。更多信息见[Extract - General Tips](#general-tips)。

在每次保存迭代时，如果整体损失下降（即模型得到改善），模型就会自动备份。如果你的模型由于某种原因损坏了，你可以进入模型文件夹，从备份中删除`.bk`扩展名，从备份中恢复模型。

你可以通过在图形用户界面的选项上悬停或通过帮助标志来查看训练的全部参数列表。

```bash
python faceswap.py train -h
```
一些插件有可配置的选项。你可以在以下内容中找到配置选项。`<faceswap_folder>config\train.ini`。你需要至少运行一次Train或GUI来生成这个文件。

# Converting a video
现在，我们对我们的训练模型感到满意，我们可以转换我们的视频。它是如何工作的？

首先，我们需要为我们的swap生成一个`alignments.json`文件。要做到这一点，请按照[提取面孔](#extracting-faces)中的步骤进行，只是这次你要对源视频中的每个面孔都运行提取。这个文件告诉转换过程，脸部在源帧上的位置。

你很可能要清理你的排列文件，删除假正例、排列不整齐的脸等等。这些在你的最终转换中看起来并不理想。有一些工具可以帮助解决这个问题。

就像提取一样，你可以从一系列的图像或视频文件中转换。

还记得我们最初的那些特朗普的照片吗？让我们试着在那里swap一张脸。我们将使用该目录作为我们的输入目录，创建一个新的文件夹，将输出保存在那里，并告诉他们使用哪个模型。

**Command Line:**
```bash
python faceswap.py convert -i ~/faceswap/src/trump/ -o ~/faceswap/converted/ -m ~/faceswap/trump_cage_model/
```

**GUI:**

![convert](https://i.imgur.com/GzX1ME2.jpg)

现在它应该开始交换所有这些图片的脸。


## General Tips
你可以通过在GUI中的选项上悬停或通过帮助标志来查看转换的全部参数列表，即。

```bash
python faceswap.py convert -h
```

一些插件有可配置的选项。你可以在以下内容中找到配置选项。`<faceswap_folder>config\convert.ini`。你将需要至少运行一次Convert或GUI来生成这个文件。

# GUI
上述所有的命令和选项都可以从GUI中运行。这是用以下方式启动的。

```bash
python faceswap.py gui
```

GUI允许一个更友好的界面进入脚本，也有一些扩展功能。将鼠标悬停在GUI中的选项上会告诉你更多关于该选项的作用。

# Video's
一个视频只是一系列帧形式的图片。因此，你可以收集其中的原始图像作为你的数据集，或者将你的结果合并成一个视频。

# EFFMPEG
你可以用内置的effmpeg工具进行各种视频处理。你可以通过运行看到全部可用的参数列表。
```bash
python tools.py effmpeg -h
```

# Extracting video frames with FFMPEG
另外，你也可以用[ffmpeg](https://www.ffmpeg.org)将一个视频分割成不同的帧，比如说。下面是一个将视频处理成独立帧的命令样本。

```bash
ffmpeg -i /path/to/my/video.mp4 /path/to/output/video-frame-%d.png
```

# Generating a video
如果你用[ffmpeg](https://www.ffmpeg.org)分割了一段视频，并把它们作为交换脸部的目标，你可以再次组合这些帧。下面的命令将png帧再次缝合成一个视频。

```bash
ffmpeg -i video-frame-%0d.png -c:v libx264 -vf "fps=25,format=yuv420p" out.mp4
```

# Notes
本指南还远未完成。功能可能会随着时间的推移而改变，而且随着时间的推移，新的依赖性也会被添加和删除。

If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) or the [FaceSwap Discord server](https://discord.gg/FdEwxXd). Usage questions raised in this repo are likely to be closed without response.
