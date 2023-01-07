# Project name
Furigoma(Piece Toss) with NVIDIA Jetson nano

# Overview
In recent years, Shogi (Japanese Chess) has been gaining momentum in Japan, and Shogi is being distributed on various video distribution platforms. ([Youtube](https://www.youtube.com/), [Abema](https://abema.tv/now-on-air/shogi), [Niconico](https://live.nicovideo.jp/), [IGO & SHOGI CHANNEL](https://www.igoshogi.net/), etc.)
Shogi can take up to two days to complete a single game, and viewers can enjoy not only the game but also a wide range of other aspects of the game.
For example, the facial expressions and gestures of the players, the meals they eat, and the traditional Shogi manners.
Among them, Furikoma(Piece Toss) is also popular.

Furikoma(Piece Toss) is a formal method of randomly determining the first and second positions in a game of shogi. It is the action of taking five Hohei(Pawn) on the board, mixing them up, and releasing them.
The front of the piece is Hohei(Pawn) and the back is Tokin(Promoted Pawn).

![Hohei(Pawn)](https://github.com/dk-flylab/furigoma/blob/main/images/ExampleTraining_hohei.JPG)
Hohei(Pawn)

![Tokin(Promoted Pawn)](https://github.com/dk-flylab/furigoma/blob/main/images/ExampleTraining_tokin.JPG)
Tokin(Promoted Pawn)

If there are many Hohei(Pawn), the higher ranked player moves his pieces first(Sente(Black)), and if there are many Tokin(Promoted Pawn) pieces, the higher ranked player moves his pieces later(Gote(White)).[(Furikoma in the 79th Meijin(Shogi master) match)](https://www.youtube.com/watch?v=LsHWH7vo8r8#t=17m10s)

This project counts the types of pieces in furikoma to determine the first and second moves of the higher-ranked players.


# AI model and Training of Deep Learning
・Algorithm : YOLO v5

・Number of training data : Approximately 4,000 sets of photos and label data.

　　※A small number of photos were resized, luminosity changed, and rotated to increase the number
