---
title: JS Audio Recorder 使用示例
---

# JS Audio Recorder 使用示例

## 基础录音示例

以下是一个基础的录音、播放和下载示例：

```html
<!DOCTYPE html>
<html>
<head>
  <title>JS Audio Recorder 基础示例</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    .btn {
      padding: 10px 15px;
      margin: 5px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }
    .btn-primary {
      background-color: #4CAF50;
      color: white;
    }
    .btn-secondary {
      background-color: #2196F3;
      color: white;
    }
    .btn-danger {
      background-color: #f44336;
      color: white;
    }
    .controls {
      margin: 20px 0;
    }
    .status {
      margin: 10px 0;
      padding: 10px;
      background-color: #f5f5f5;
      border-radius: 4px;
    }
  </style>
</head>
<body>
  <h1>JS Audio Recorder 基础示例</h1>
  
  <div class="controls">
    <button id="startBtn" class="btn btn-primary">开始录音</button>
    <button id="pauseBtn" class="btn btn-secondary" disabled>暂停录音</button>
    <button id="resumeBtn" class="btn btn-secondary" disabled>恢复录音</button>
    <button id="stopBtn" class="btn btn-danger" disabled>停止录音</button>
  </div>
  
  <div class="controls">
    <button id="playBtn" class="btn btn-secondary" disabled>播放录音</button>
    <button id="pausePlayBtn" class="btn btn-secondary" disabled>暂停播放</button>
    <button id="stopPlayBtn" class="btn btn-secondary" disabled>停止播放</button>
    <button id="downloadBtn" class="btn btn-primary" disabled>下载录音</button>
  </div>
  
  <div class="status" id="status">状态：等待开始录音</div>
  
  <script src="https://cdn.jsdelivr.net/npm/js-audio-recorder@1.0.7/dist/recorder.min.js"></script>
  <script>
    // 获取DOM元素
    const startBtn = document.getElementById('startBtn');
    const pauseBtn = document.getElementById('pauseBtn');
    const resumeBtn = document.getElementById('resumeBtn');
    const stopBtn = document.getElementById('stopBtn');
    const playBtn = document.getElementById('playBtn');
    const pausePlayBtn = document.getElementById('pausePlayBtn');
    const stopPlayBtn = document.getElementById('stopPlayBtn');
    const downloadBtn = document.getElementById('downloadBtn');
    const statusDiv = document.getElementById('status');
    
    // 创建录音实例
    const recorder = new Recorder({
      sampleBits: 16,
      sampleRate: 44100,
      numChannels: 1
    });
    
    // 更新状态显示
    function updateStatus(message) {
      statusDiv.textContent = '状态：' + message;
    }
    
    // 开始录音
    startBtn.addEventListener('click', () => {
      recorder.start().then(() => {
        updateStatus('正在录音...');
        startBtn.disabled = true;
        pauseBtn.disabled = false;
        stopBtn.disabled = false;
        resumeBtn.disabled = true;
      }).catch(error => {
        updateStatus('录音失败: ' + error.message);
        console.error('录音失败:', error);
      });
    });
    
    // 暂停录音
    pauseBtn.addEventListener('click', () => {
      recorder.pause();
      updateStatus('录音已暂停');
      pauseBtn.disabled = true;
      resumeBtn.disabled = false;
    });
    
    // 恢复录音
    resumeBtn.addEventListener('click', () => {
      recorder.resume();
      updateStatus('正在录音...');
      pauseBtn.disabled = false;
      resumeBtn.disabled = true;
    });
    
    // 停止录音
    stopBtn.addEventListener('click', () => {
      recorder.stop();
      updateStatus('录音已停止，可以播放或下载');
      startBtn.disabled = false;
      pauseBtn.disabled = true;
      resumeBtn.disabled = true;
      stopBtn.disabled = true;
      playBtn.disabled = false;
      downloadBtn.disabled = false;
    });
    
    // 播放录音
    playBtn.addEventListener('click', () => {
      recorder.play();
      updateStatus('正在播放录音...');
      playBtn.disabled = true;
      pausePlayBtn.disabled = false;
      stopPlayBtn.disabled = false;
    });
    
    // 暂停播放
    pausePlayBtn.addEventListener('click', () => {
      recorder.pausePlay();
      updateStatus('播放已暂停');
      pausePlayBtn.disabled = true;
      playBtn.disabled = false;
    });
    
    // 停止播放
    stopPlayBtn.addEventListener('click', () => {
      recorder.stopPlay();
      updateStatus('播放已停止');
      playBtn.disabled = false;
      pausePlayBtn.disabled = true;
      stopPlayBtn.disabled = true;
    });
    
    // 下载录音
    downloadBtn.addEventListener('click', () => {
      // 获取WAV格式的Blob对象
      const wavBlob = recorder.getWAVBlob();
      
      // 创建下载链接
      const url = URL.createObjectURL(wavBlob);
      const link = document.createElement('a');
      link.href = url;
      link.download = 'recording_' + new Date().getTime() + '.wav';
      link.click();
      
      updateStatus('录音已下载');
    });
  </script>
</body>
</html>
```

## 音量可视化示例

以下示例展示了如何实时显示录音的音量：

```html
<!DOCTYPE html>
<html>
<head>
  <title>JS Audio Recorder 音量可视化</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    .btn {
      padding: 10px 15px;
      margin: 5px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }
    .btn-primary {
      background-color: #4CAF50;
      color: white;
    }
    .btn-danger {
      background-color: #f44336;
      color: white;
    }
    .controls {
      margin: 20px 0;
    }
    .volume-container {
      margin: 20px 0;
      background-color: #f5f5f5;
      border-radius: 4px;
      height: 30px;
      position: relative;
    }
    .volume-bar {
      height: 100%;
      width: 0;
      background-color: #4CAF50;
      border-radius: 4px;
      transition: width 0.1s ease;
    }
    .volume-text {
      position: absolute;
      right: 10px;
      top: 5px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <h1>JS Audio Recorder 音量可视化</h1>
  
  <div class="controls">
    <button id="startBtn" class="btn btn-primary">开始录音</button>
    <button id="stopBtn" class="btn btn-danger" disabled>停止录音</button>
  </div>
  
  <div class="volume-container">
    <div id="volumeBar" class="volume-bar"></div>
    <div id="volumeText" class="volume-text">0</div>
  </div>
  
  <script src="https://cdn.jsdelivr.net/npm/js-audio-recorder@1.0.7/dist/recorder.min.js"></script>
  <script>
    // 获取DOM元素
    const startBtn = document.getElementById('startBtn');
    const stopBtn = document.getElementById('stopBtn');
    const volumeBar = document.getElementById('volumeBar');
    const volumeText = document.getElementById('volumeText');
    
    // 创建录音实例
    const recorder = new Recorder({
      sampleBits: 16,
      sampleRate: 44100,
      numChannels: 1,
      // 开启音量监控
      audioVolume: true
    });
    
    let volumeInterval = null;
    
    // 开始录音并监控音量
    startBtn.addEventListener('click', () => {
      recorder.start().then(() => {
        startBtn.disabled = true;
        stopBtn.disabled = false;
        
        // 每100毫秒获取一次音量
        volumeInterval = setInterval(() => {
          // 获取音量，范围0-100
          const volume = recorder.getVolume();
          
          // 更新音量条
          volumeBar.style.width = volume + '%';
          volumeText.textContent = Math.round(volume);
          
          // 根据音量改变颜色
          if (volume < 30) {
            volumeBar.style.backgroundColor = '#4CAF50'; // 绿色
          } else if (volume < 70) {
            volumeBar.style.backgroundColor = '#FFC107'; // 黄色
          } else {
            volumeBar.style.backgroundColor = '#F44336'; // 红色
          }
        }, 100);
      }).catch(error => {
        console.error('录音失败:', error);
      });
    });
    
    // 停止录音
    stopBtn.addEventListener('click', () => {
      recorder.stop();
      clearInterval(volumeInterval);
      startBtn.disabled = false;
      stopBtn.disabled = true;
    });
  </script>
</body>
</html>
```

## 录音波形可视化

以下示例展示了如何使用Canvas绘制录音波形：

```html
<!DOCTYPE html>
<html>
<head>
  <title>JS Audio Recorder 波形可视化</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    .btn {
      padding: 10px 15px;
      margin: 5px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }
    .btn-primary {
      background-color: #4CAF50;
      color: white;
    }
    .btn-danger {
      background-color: #f44336;
      color: white;
    }
    .controls {
      margin: 20px 0;
    }
    canvas {
      width: 100%;
      height: 200px;
      background-color: #f5f5f5;
      border-radius: 4px;
    }
  </style>
</head>
<body>
  <h1>JS Audio Recorder 波形可视化</h1>
  
  <div class="controls">
    <button id="startBtn" class="btn btn-primary">开始录音</button>
    <button id="stopBtn" class="btn btn-danger" disabled>停止录音</button>
  </div>
  
  <canvas id="waveform"></canvas>
  
  <script src="https://cdn.jsdelivr.net/npm/js-audio-recorder@1.0.7/dist/recorder.min.js"></script>
  <script>
    // 获取DOM元素
    const startBtn =