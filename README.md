
[![License](https://img.shields.io/badge/License-View%20License-blue.svg)](https://github.com/GuijiAI/HeyGem.ai/blob/main/LICENSE)
![Python](https://img.shields.io/badge/Python-3.8-blue.svg)
![Linux](https://img.shields.io/badge/OS-Linux-brightgreen.svg)


---


<a name="chinese-version"></a>

# heygem-gen-video

## 项目简介

heygem-gen-video 是一个基于 Python 的数字人项目，它从 [HeyGem.ai](https://github.com/GuijiAI/HeyGem.ai) 中提取出来，它能够直接在 Linux 系统上运行，摆脱了对 Docker 和 Windows 系统的依赖。我们的目标是提供一个更易于部署和使用的数字人解决方案。   

[RTX 50版本已经发布，点击可达](https://github.com/wangshaojie1995/heygem-gen-video-5090)  

**如果你觉得这个项目对你有帮助，欢迎给我们 Star！**  
**如果运行过程中遇到问题，在查阅已有 Issue 后，在查阅 Google/baidu/ai 后，欢迎提交 Issues！**  
**本项目中，所有 .so 文件均由硅基编译，与开发者无关**  
**本项目中，所有模型均由硅基提供，与开发者无关**  

## 主要特性

* 无需 Docker: 直接在 Linux 系统上运行，简化部署流程。
* 无需 Windows: 完全基于 Linux 开发和测试。
* Python 驱动: 使用 Python 语言开发，易于理解和扩展。
* 开发者友好: 易于使用和扩展。
* 完全离线。  
* 紧包含数字人合成，不包含声音克隆和文字转语音
* 紧随Heygem官方更新

[云端部署](https://www.xiangongyun.com/register/G3F36A)

微信群  
![](https://github.com/wangshaojie1995/heygem-gen-video-5090/blob/main/contact_qr.png)

## 开始使用

### 安装
#### 环境 
本项目**支持且仅支持 Linux & python3.8 环境**  
请确保你的 Linux 系统上已经安装了 **Python 3.8**。然后，使用 pip 安装项目依赖项  
**备用** 同时也提供一个备用的环境 [requirements_0.txt](requirements_0.txt)，遇到问题的话，你可以参考它来建立一个新的环境。  
**具体的 onnxruntime-gpu / torch 等需要结合你的机器上的 cuda 版本去尝试一些组合，否则仍旧可能遇到问题。**  
**请尽量不要询问任何关于 pip 的问题，感谢合作**


```bash
# 直接安装整个 requirements.txt 不一定成功，更建议跑代码观察报错信息，然后根据报错信息结合 requirements 去尝试安装，祝你顺利。
# pip install -r requirements.txt
```

### 使用
把项目克隆到本地
```bash
wget https://github.com/wangshaojie1995/heygem-gen-video/releases/download/20250602/heygem.tar.gz
tar -xzvf /path/to/your/heygem.tar.gz
cd heygem
```
#### API使用 command:
```bash
python app_local.py 
```  

* API文档

### 视频合成

- 合成接口：`http://127.0.0.1:8383/easy/submit`

  ```json
  // 请求参数
  {
    "audio_url": "{audioPath}", // 音频路径
    "video_url": "{videoPath}", // 视频路径
    "code": "{uuid}", // 唯一key
    "chaofen": 0, // 固定值
    "watermark_switch": 0, // 固定值
    "pn": 1 // 固定值
  }
  ```

- 进度查询：`http://127.0.0.1:8383/easy/query?code=${taskCode}`
  > get 请求，参数`taskCode`是上面合成接口入参中的`code`


#### gradio:  
```bash
python app.py
# 请等待模型初始化完成后提交任务
```

## QA
### 1. 多个人脸报错  
下载新的人脸检测模型，替换原本的人脸检测模型或许可以解决。
```bash
wget https://github.com/wangshaojie1995/heygem-gen-video-5090/blob/main/scrfd_10g_kps.onnx
mv face_detect_utils/resources/scrfd_500m_bnkps_shape640x640.onnx face_detect_utils/resources/scrfd_500m_bnkps_shape640x640.onnx.bak
mv scrfd_10g_kps.onnx face_detect_utils/resources/scrfd_500m_bnkps_shape640x640.onnx
```

### 2. ImportError: cannot import name check_argument_types  
缺包
```bash
pip install typeguard
```
  
### 3. library.so 找不到  
报错一般是类似于 Could not load library libcublasLt.so.11. Error: libcublasLt.so.11: cannot open shared object file: No such file or directory  

执行以下命令查看是否有改文件  
```
sudo find /usr -name "libcublasLt.so.11"  
```
没有的话，应该需要安装对应版本的cuda  
如果有的话就把第一步查看的文件路径添加到环境变量  
```
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
永久生效就添加到 ~/.bashrc 里面然后 source ~/.bashrc 一下  

## Contributing  
欢迎贡献！

## License
参考 heyGem.ai 的协议.
