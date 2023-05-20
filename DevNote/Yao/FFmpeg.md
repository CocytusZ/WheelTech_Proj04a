# Ffmpeg

## 输入查看视频信息

```{.bat}
ffmpeg -i <targetVideo>

```

## 裁剪视频画面

```{.bat}
ffmpeg -i input.mp4 -vf "crop=w:h:x:y" output.mp4

```

在上述命令中，你需要根据实际情况调整参数的值：

input.mp4 是输入视频文件的名称。
output.mp4 是输出视频文件的名称。
对于裁剪操作，你需要指定以下参数：

w 是裁剪后的目标宽度。
h 是裁剪后的目标高度。
x 是裁剪区域的起始 x 坐标。
y 是裁剪区域的起始 y 坐标。


## 剪辑视频
```{.bat}
ffmpeg -i input.mp4 -ss 00:00:10 -t 00:00:20 -c copy output.mp4
```

上述命令将从 input.mp4 视频文件中提取从第 10 秒开始持续 20 秒的片段，并将其保存为 output.mp4。

解释一下参数的含义：

-i input.mp4：指定输入视频文件。
-ss 00:00:10：设置开始时间为 10 秒。
-t 00:00:20：设置持续时间为 20 秒。
-c copy：使用原始视频和音频编解码器进行拷贝，以保持原始质量和格式。
output.mp4：指定输出视频文件。

## 视频转格式（以mp4为例）

```{.bat}
ffmpeg -i input_video -c:v libx264 -c:a aac output.mp4
```

在上述命令中，input_video 是你要转换的视频文件名，output.mp4 是转换后的输出文件名。

这个命令使用了默认的编码器来进行视频和音频的转码。视频编码器是 libx264，音频编码器是 AAC。如果你希望使用其他编码器，可以更换对应的参数。