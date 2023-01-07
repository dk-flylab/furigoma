# Project name
Furigoma(Piece Toss) with NVIDIA Jetson nano

# Overview
In recent years, Shogi (Japanese Chess) has been gaining momentum in Japan, and Shogi is being distributed on various video distribution platforms. ([Youtube](https://www.youtube.com/), [Abema](https://abema.tv/now-on-air/shogi), [Niconico](https://live.nicovideo.jp/), [IGO & SHOGI CHANNEL](https://www.igoshogi.net/), etc.)
Shogi can take up to two days to complete a single game, and viewers can enjoy not only the game but also a wide range of other aspects of the game.
For example, the facial expressions and gestures of the players, the meals they eat, and the traditional Shogi manners.
Among them, Furikoma(Piece Toss) is also popular.

Furikoma is the formal method of randomly determining the order of play in a game of Shogi. It is the action of taking five Hohei(Pawn) on the board, mixing them up, and releasing them.
The front of the piece is Hohei(Pawn) and the back is Tokin(Promoted Pawn).

![Hohei(Pawn)](https://github.com/dk-flylab/furigoma/blob/main/images/ExampleTraining_hohei.JPG)
Hohei(Pawn)

![Tokin(Promoted Pawn)](https://github.com/dk-flylab/furigoma/blob/main/images/ExampleTraining_tokin.JPG)
Tokin(Promoted Pawn)

If there are many Hohei(Pawn), the higher ranked player moves his pieces first(Sente(Black)), and if there are many Tokin(Promoted Pawn) pieces, the higher ranked player moves his pieces later(Gote(White)).[(Furikoma in the 79th Meijin(Shogi master) match)](https://www.youtube.com/watch?v=LsHWH7vo8r8#t=17m10s)

In this project, we determine turn the higher-ranked player the by counting the types of pieces

# AI model and Training of Deep Learning
・Model : [YOLOv5s](https://github.com/ultralytics/yolov5#pretrained-checkpoints)

・Number of training data : Approximately 4,000 sets with Hohei and Tokin of photos and label data.
 - A small number of photos were resized, luminosity changed, and rotated to increase the number.
 
 ![data](https://github.com/dk-flylab/furigoma/blob/main/images/data%20.png)
 
 - Labeling range specification was automated by detecting the edge of the piece.
 
![edge](https://github.com/dk-flylab/furigoma/blob/main/images/edge.gif)

Video of automatic range setting results
 
・Training epoch : 100

`python train.py --img 640 --batch 64 --epochs 100 --data '/content/drive/MyDrive/furigoma.yaml' --name furigoma --cfg ./models/yolov5s.yaml --weights yolov5s.pt`

![results](https://github.com/dk-flylab/furigoma/blob/main/images/results.png)
Learning was done using [Google Colaboratory](https://colab.research.google.com/).

# Edge System
・Hardware : Edge device is NVIDIA Jetson Nano, and video source is USB Camera of Logicool C270n.

・Sosftware : Modified based on Yolov5's detect.py.　Added counting of piece types and determining the order of t higher ranked player.

Picture of the edge system is here.

![EdgeSystem](https://github.com/dk-flylab/furigoma/blob/main/images/EdgeSystem.jpg)

# DEMO
There is [FULL VIDEO](https://www.youtube.com/watch?v=eqqjcI9cLNg) the Edge system running. It uses a fast processing model(YOLOv5s), and detection accuracy is not high. However, we believe that the results are sufficiently good for practical use.

Below are examples of successful detection and determination.

![Sente](https://github.com/dk-flylab/furigoma/blob/main/images/sente.gif)　Sente(Black)

![Gote](https://github.com/dk-flylab/furigoma/blob/main/images/gote.gif)　Gote(White)

# Setup to Run
・Jetson

Prepareing hardwares are as follows and Connecting them like a picture.
 - Jetson Nano
 - USB Camera(Logicool C270n)
 - Display
 - Keyboard
 - Mouse
 - Wireless LAN module
 - Power Supply
 
![jetson](https://github.com/dk-flylab/furigoma/blob/main/images/jetson_nano.png)

・JetPack

JetPack 4.6.3 is [here](https://developer.nvidia.com/jetpack-sdk-463). Downloading For "Jetson Nano Developer Kit" Version and installing it through the [instruction](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write).

・Installing Yolov5

Installing Yolov5 through the [instruction](https://github.com/ultralytics/yolov5).

・Get and Run the Project

Store model.pt and detect_furigoma.py in the Yolov5 directory and execute the following command

`python3 detect_furigoma.py --source 0 --weight model.pt`

# Acknowledgments
I've learned AI from this [book](https://www.amazon.co.jp/Jetson-Nano-%E8%B6%85%E5%85%A5%E9%96%80-%E6%94%B9%E8%A8%82%E7%AC%AC2%E7%89%88-Japan-Group-ebook/dp/B092LY4HN9/ref=sr_1_1?crid=338JVODRS3E1K&keywords=jetson+%E6%9C%AC&qid=1673102318&sprefix=jetson+honn%2Caps%2C178&sr=8-1).
