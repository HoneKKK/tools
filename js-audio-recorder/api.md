---
title: JS Audio Recorder API参考
---

# JS Audio Recorder API参考

## 基本用法

JS Audio Recorder的基本使用方法如下：

```javascript
// 创建录音实例
const recorder = new Recorder([options]);

// 开始录音
recorder.start();

// 暂停录音
recorder.pause();

// 恢复录音
recorder.resume();

// 停止录音
recorder.stop();

// 播放录音
recorder.play();

// 停止播放
recorder.stopPlay();
```

## 构造函数选项

创建Recorder实例时，可以传入以下配置选项：

```javascript
const recorder = new Recorder({
  sampleBits: 16,         // 采样位数，支持8或16，默认是16
  sampleRate: 48000,       // 采样率，支持11025、16000、22050、24000、44100、48000，默认是48000
  numChannels: 1,         // 声道，支持1或2，默认是1
  compiling: false,       // 是否边录边转换，默认是false
});
```

## 实例方法

### 录音控制

#### start()

开始录音。返回Promise对象。

```javascript
recorder.start().then(() => {
  console.log('开始录音');
}).catch(error => {
  console.error('录音失败: ', error);
});
```

#### pause()

暂停录音。

```javascript
recorder.pause();
```

#### resume()

恢复录音。

```javascript
recorder.resume();
```

#### stop()

停止录音。

```javascript
recorder.stop();
```

### 播放控制

#### play()

播放录音。

```javascript
recorder.play();
```

#### pausePlay()

暂停播放。

```javascript
recorder.pausePlay();
```

#### resumePlay()

恢复播放。

```javascript
recorder.resumePlay();
```

#### stopPlay()

停止播放。