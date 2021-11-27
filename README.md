# deepfakes_faceswap
<p align="center">
  <a href="https://faceswap.dev"><img src="https://i.imgur.com/zHvjHnb.png"></img></a>
<br />FaceSwap是一个利用深度学习来识别和交换图片和视频中人脸的工具。
</p>
<p align="center">
<img src = "https://i.imgur.com/nWHFLDf.jpg"></img>
</p>

<p align="center">
<a href="https://www.patreon.com/bePatron?u=23238350"><img src="https://c5.patreon.com/external/logo/become_a_patron_button.png"></img></a>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="https://discord.gg/FC54sYg"><img src="https://i.imgur.com/gIpztkv.png"></img></a></p>
<p align="center">
  <a href="https://www.youtube.com/watch?v=r1jng79a5xc"><img src="https://img.youtube.com/vi/r1jng79a5xc/0.jpg"></img></a>
<br />Jennifer Lawrence/Steve Buscemi FaceSwap using the Villain model
</p>

[![Build Status](https://travis-ci.org/deepfakes/faceswap.svg?branch=master)](https://travis-ci.org/deepfakes/faceswap) [![Documentation Status](https://readthedocs.org/projects/faceswap/badge/?version=latest)](https://faceswap.readthedocs.io/en/latest/?badge=latest)

Make sure you check out [INSTALL.md](INSTALL.md) before getting started.

- [deepfakes_faceswap](#deepfakesfaceswap)
- [Manifesto](#manifesto)
  - [FaceSwap has ethical uses.](#faceswap-has-ethical-uses)
- [How To setup and run the project](#how-to-setup-and-run-the-project)
- [Overview](#overview)
  - [Extract](#extract)
  - [Train](#train)
  - [Convert](#convert)
  - [GUI](#gui)
- [General notes:](#general-notes)
- [Help I need support!](#help-i-need-support)
  - [Discord Server](#discord-server)
  - [FaceSwap Forum](#faceswap-forum)
- [Donate](#donate)
  - [Patreon](#patreon)
  - [One time Donations](#one-time-donations)
    - [@torzdf](#torzdf)
    - [@andenixa](#andenixa)
    - [@kvrooman](#kvrooman)
- [How to contribute](#how-to-contribute)
  - [For people interested in the generative models](#for-people-interested-in-the-generative-models)
  - [For devs](#for-devs)
  - [For non-dev advanced users](#for-non-dev-advanced-users)
  - [For end-users](#for-end-users)
  - [For haters](#for-haters)
- [About github.com/deepfakes](#about-githubcomdeepfakes)
  - [What is this repo?](#what-is-this-repo)
  - [Why this repo?](#why-this-repo)
  - [Why is it named 'deepfakes' if it is not /u/deepfakes?](#why-is-it-named-deepfakes-if-it-is-not-udeepfakes)
  - [What if /u/deepfakes feels bad about that?](#what-if-udeepfakes-feels-bad-about-that)
- [About machine learning](#about-machine-learning)
  - [How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?](#how-does-a-computer-know-how-to-recognizeshape-faces-how-does-machine-learning-work-what-is-a-neural-network)

# Manifesto

## FaceSwap道德方面。
当换脸技术第一次被开发和发表时，这项技术是开创性的，它是人工智能发展的一个巨大步。
它也被学术界以外的人完全忽视，因为代码是混乱和零散的。
它需要对复杂的人工智能技术有透彻的了解，并且需要花费大量的精力来弄清楚。
直到有个人把它汇集成一个单一的、有凝聚力的集合。
它运行了，工作了，就像互联网上出现的新技术一样，它立即被用来创造不适当的内容。
尽管该软件最初被赋予了不恰当的用途，但它是第一个任何人都可以下载、运行并通过实验学习的人工智能代码，而无需拥有数学、计算机理论、心理学等方面的博士学位。
在 "深度造假 "之前，这些技术就像黑魔法一样，只有那些能够理解深奥和无尽复杂的书籍和论文中所描述的所有内部运作的人，才会去实践。
"Deepfakes "改变了这一切，任何人都可以参与AI开发。
对我们这些开发者来说，这段代码的发布开启了一个奇妙的学习机会。
它使我们能够在其他人开发的想法的基础上，与各种熟练的编码员合作，在学习新技能的同时尝试人工智能，并最终为一项新兴的技术做出贡献，随着它的发展，它将看到更多的主流应用。
是否有一些人在用类似的软件做可怕的事情？是的。
也正因为如此，开发人员一直在严格遵守道德标准。
我们中的许多人甚至不使用它来创建视频，我们只是修补代码，看看它能做什么。
可悲的是，媒体只集中在这个软件的不道德用途上。不幸的是，这是它第一次暴露在公众面前的性质，但这并不代表它被创造的原因，我们现在如何使用它，或者我们看到它的未来。
像任何技术一样，它可以被用来做好事，也可以被滥用。
我们打算在开发FaceSwap的过程中，尽量减少它被滥用的可能性，同时最大限度地发挥它作为学习、实验以及合法换脸的工具的潜力。

我们并不是要诋毁名人或贬低任何人。我们是程序员，我们是工程师，我们是好莱坞VFX艺术家，我们是活动家，我们是业余爱好者，我们是人类。
为此，我们觉得现在是时候对这个软件是什么和不是什么做出一个标准声明了，就我们这些开发者而言。

- FaceSwap不是为了创造不适当的内容。
- FaceSwap不用于未经同意或意图隐瞒而改变面孔的行为。
- FaceSwap不是为了任何非法的、不道德的或有问题的目的。
- FaceSwap的存在是为了实验和发现人工智能技术，用于社会或政治评论，用于电影，以及用于任何数量的道德和合理的用途。

我们对FaceSwap可以被用来做不道德和不光彩的事情感到非常不安。
然而，我们支持开发可以道德地使用的工具和技术，以及为任何想亲身学习的人提供人工智能方面的教育和经验。
我们将对任何将此软件用于任何不道德的目的的人采取零容忍的态度，并将积极阻止任何此类使用。

# 如何设置和运行项目
FaceSwap是一个Python程序，可以在多个操作系统上运行，包括Windows、Linux和MacOS。
参见[INSTALL.md](INSTALL.md)获取完整的安装说明。你将需要一个支持CUDA的现代GPU以获得最佳性能。AMD的GPU被部分支持。


# Overview
该项目有多个进入点。你将不得不
 - 收集照片和/或视频
 - 从你的原始照片中提取人脸
 - 在从照片/视频中提取的人脸上训练一个模型
 - 用模型转换你的来源

请查看[USAGE.md](USAGE.md)，了解更详细的说明。

## Extract
从你的设置文件夹，运行`python faceswap.py extract`。这将从`src`文件夹中获取照片，并将面孔提取到`extract`文件夹。

## Train
从你的设置文件夹，运行`python faceswap.py train`。这将从两个文件夹中获取照片，其中包含两张脸的图片，并训练一个模型，该模型将保存在`models`文件夹中。

## Convert
从你的设置文件夹，运行`python faceswap.py convert`。这将从`原始`文件夹中获取照片，并将新的面孔应用于`修改`文件夹。

## GUI
或者，你可以通过运行`python faceswap.py gui`来运行图形用户界面。

# General notes:
- 所有提到的脚本都有`-h`/`-help`选项，它们会接受参数。你很聪明，你可以弄清楚这是如何工作的，对吗！？
NB：有一个视频的转换工具。这可以通过运行`python tools.py effmpeg -h`来实现。
  另外，你可以使用[ffmpeg](https://www.ffmpeg.org)将视频转换为照片，处理图像，并将图像转换回视频。


**Some tips:**
重用现有的模型会比从零开始训练快得多。
如果没有足够的训练数据，就从看起来相似的人开始，然后再换数据。

# Help I need support!
## Discord Server
你最好的选择是加入[FaceSwap Discord server](https://discord.gg/FC54sYg)，那里有很多用户愿意提供帮助。请注意，和这个软件一样，这也是一个SFW服务器

## FaceSwap Forum
另外，你也可以在[FaceSwap论坛]（https://faceswap.dev/forum）上发表问题。请不要在这个论坛上发布一般的支持问题，因为这些问题可能会在没有回应的情况下被删除。

# Donate
The developers work tirelessly to improve and develop FaceSwap. Many hours have been put in to provide the software as it is today, but this is an extremely time-consuming process with no financial reward. If you enjoy using the software, please consider donating to the devs, so they can spend more time implementing improvements.

## Patreon
The best way to support us is through our Patreon page:

[![become-a-patron](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/bePatron?u=23238350)

## One time Donations
Alternatively you can give a one off donation to any of our Devs:
### @torzdf
 There is very little FaceSwap code that hasn't been touched by torzdf. He is responsible for implementing the GUI, FAN aligner, MTCNN detector and porting the Villain, DFL-H128 and DFaker models to FaceSwap, as well as significantly improving many areas of the code.

**Bitcoin:** bc1qpm22suz59ylzk0j7qk5e4c7cnkjmve2rmtrnc6

**Ethereum:** 0xd3e954dC241B87C4E8E1A801ada485DC1d530F01

**Monero:** 45dLrtQZ2pkHizBpt3P3yyJKkhcFHnhfNYPMSnz3yVEbdWm3Hj6Kr5TgmGAn3Far8LVaQf1th2n3DJVTRkfeB5ZkHxWozSX

**Paypal:** [![torzdf](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JZ8PP3YE9J62L)

### @andenixa
Creator of the Unbalanced and OHR models, as well as expanding various capabilities within the training process. Andenixa is currently working on new models and will take requests for donations.

**Paypal:** [![andenixa](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=NRVLQYGS6NWTU)

# How to contribute

## For people interested in the generative models
 - Go to the 'faceswap-model' to discuss/suggest/commit alternatives to the current algorithm.

## For devs
 -  完全阅读此README
 - fork 该 repo
 - 使用它
 - 检查带有 "dev "标签的问题
 - 对于那些对计算机视觉和openCV更感兴趣的开发者，请查看带有 "opencv "标签的问题。也可以自由地添加你自己的替代方案/改进措施

## For non-dev advanced users
 - 完全阅读此README
 - 克隆该版本
 - 使用它
 - 用'advuser'标签检查问题
 - 也可以去'[换脸论坛](https://faceswap.dev/forum)'，帮助别人。

## For end-users
 - 如果可以的话，在这里获取代码并进行使用
 - 你也可以去[换脸论坛](https://faceswap.dev/forum)，帮助或得到别人的帮助。
 - 要有耐心。这对开发者来说也是一个相对较新的技术。为了使这个程序对普通用户来说容易使用，已经投入了很多努力。这只是需要时间!
 - **注意**任何与运行代码有关的问题都必须在[faceswap论坛](https://faceswap.dev/forum)上打开!

## For haters
Sorry, no time for that.

# About github.com/deepfakes

## What is this repo?
It is a community repository for active users.

## Why this repo?
The joshua-wu repo seems not active. Simple bugs like missing _http://_ in front of urls have not been solved since days.

## Why is it named 'deepfakes' if it is not /u/deepfakes?
 1. 因为随着项目的发展，打错字的情况迟早会发生。
 2. 因为我们想确认原作者的身份
 3. 因为这将更好地联合贡献者和用户


## What if /u/deepfakes feels bad about that?
这是一个友好的typosquat，它完全致力于该项目。如果/u/deepfakes想接管这个 repo/用户并推动这个项目，我们欢迎他这样做（提出一个问题，我们会在Reddit上联系他）。请不要向/u/deepfakes发送消息，寻求对你在这里找到的代码的帮助。

# About machine learning

## How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?
It's complicated. Here's a good video that makes the process understandable:
[![How Machines Learn](https://img.youtube.com/vi/R9OHn5ZF4Uo/0.jpg)](https://www.youtube.com/watch?v=R9OHn5ZF4Uo)

Here's a slightly more in depth video that tries to explain the basic functioning of a neural network:
[![How Machines Learn](https://img.youtube.com/vi/aircAruvnKk/0.jpg)](https://www.youtube.com/watch?v=aircAruvnKk)

tl;dr: training data + trial and error
