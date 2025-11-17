# AI康复训练平台

一个集机器人技术、视频技术、语音识别、人工智能于一体的开源综合平台，专为多场景康复训练而设计。它支持包括上肢、下肢和失语症训练在内的各种康复项目，采用前后端分离架构，提供多语言支持和无缝硬件集成能力。

该项目根据 MIT 许可证获得许可 - 有关详细信息，请参阅 [LICENSE]文件

[AI康复训练平台](#ai康复训练平台)
- [AI康复训练平台](#ai康复训练平台)
  - [✨ 主要特点](#-主要特点)
  - [✨ 项目截图 / 演示 GIF](#-项目截图--演示-gif)
  - [📋 技术架构](#-技术架构)
  - [🚀 快速入门](#-快速入门)
    - [先决条件](#先决条件)
    - [安装步骤](#安装步骤)
  - [📂 目录结构](#-目录结构)
  - [🔌 核心 API 接口](#-核心-api-接口)
    - [AI分析](#ai分析)
    - [患者管理](#患者管理)
  - [🤖 硬件集成](#-硬件集成)
  - [📱 演示与支持](#-演示与支持)
  - [📱 项目未来计划](#-项目未来计划)
  - [👥 贡献指南](#-贡献指南)
  - [⚠️ 常见问题](#️-常见问题)
  - [🔒 安全与隐私](#-安全与隐私)
  - [📄 许可证](#-许可证)
  - [🧑💻 作者 \& 隶属关系](#-作者--隶属关系)


## ✨ 主要特点

- 智能生成训练计划，个性化难度适应

- 实时人体姿势识别和纠正反馈（由 MediaPipe + 视频技术提供支持）

- 人工智能驱动的失语症康复语音分析（发音评估+改进建议）

- 无缝机器人和硬件集成（蓝牙/串行端口通信）

- 全面的训练统计和成就解锁系统

- 双语支持（中文/英文）和跨平台体验（网页+移动）

## ✨ 项目截图 / 演示 GIF
- 平台前端页面截图如下：
![images](/images//1.png)
 
- 机器人运行视频/GIF如下：
![images](/images/2-1.gif)
 


## 📋 技术架构

|模块|技术与工具|
|---|---|
|**后端**|Python 3.10+、FastAPI、SQLServer、TensorFlow、Vosk、pydub、librosa|
|**前端**|HTML5、JavaScript（原生/ES6）、Tailwind CSS、Font Awesome、Chart.js、MediaPipe|
|**硬件**|ESP32、Arduino/C++、  Stepper Motors, Bluetooth Modules|
|**部署**|Nginx、Docker Compose|

|**系统架构图**|
![images](/images/jiagou.png)

## 🚀 快速入门

### 先决条件

- 已安装 Python 3.10+

- 已安装 Git

- 带有 Live Server 扩展的 VSCode（推荐）

- ESP32 开发环境（用于硬件集成）

### 安装步骤

1. **克隆仓库**'git clone https://github.com/your-username/ai-rehabilitation-training-platform.git
CD 人工智能康复培训平台”

2. **安装后端依赖项**
3. pip install -r requirements.txt' absl-py==2.3.1
annotated-types==0.7.0
anyio==4.11.0
astunparse==1.6.3
certifi==2025.10.5
charset-normalizer==3.4.3
click==8.3.0
colorama==0.4.6
fastapi==0.119.0
flatbuffers==25.9.23
gast==0.6.0
google-pasta==0.2.0
grpcio==1.75.1
h11==0.16.0
h5py==3.15.0
idna==3.11
keras==3.11.3
libclang==18.1.1
Markdown==3.9
markdown-it-py==4.0.0
MarkupSafe==3.0.3
mdurl==0.1.2
ml_dtypes==0.5.3
namex==0.1.0
numpy==2.3.3
opt_einsum==3.4.0
optree==0.17.0
packaging==25.0
pillow==11.3.0
protobuf==6.32.1
pydantic==2.12.0
pydantic_core==2.41.1
Pygments==2.19.2
python-multipart==0.0.20
requests==2.32.5
rich==14.2.0
six==1.17.0
sniffio==1.3.1
starlette==0.48.0
tensorboard==2.20.0
tensorboard-data-server==0.7.2
tensorflow==2.20.0
termcolor==3.1.0
typing-inspection==0.4.2
typing_extensions==4.15.0
urllib3==2.5.0
uvicorn==0.37.0
Werkzeug==3.1.3
wrapt==1.17.3
sqlalchemy==2.0.23
pyodbc==5.0.1
python-dotenv==1.0.0
python-jose[cryptography]==3.3.0
PyJWT==2.8.0
passlib==1.7.4
jinja2==3.1.2
bcrypt==3.2.2 
python-dateutil==2.8.2
Flask==2.3.3
librosa>=0.10.0
vosk>=0.3.45
pydub>=0.25.1

4. **•Nginx反向代理配置**
   #配置代码
   server {
    server_name  www.bnstw.com bnstw.com;
    location /ai/frontend/ {
        alias /home/ubuntu/ai/frontend/;
        index index.html index.htm;
        try_files $uri $uri/ /ai/frontend/index.html;
        location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
            expires 1y;
            add_header Cache-Control "public, immutable";
            access_log off;
        }
    }
    location /api {
        proxy_pass http://127.0.0.1:8000/api; 
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme; 
    }    
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
     location /ai/docs/ {
        alias /home/ubuntu/ai/docs/;
        autoindex on;
        types {
            video/mp4 mp4;
            application/pdf pdf;
            text/plain txt;
            text/html html;
        }
        location ~* \.(mp4|pdf|txt|html)$ {
            add_header Access-Control-Allow-Origin *;
            expires 1h;
            add_header X-Content-Type-Options nosniff;
        }
    }
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/bnstw.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/bnstw.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
server {
    if ($host = www.bnstw.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    if ($host = bnstw.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    listen 80;
    server_name  www.bnstw.com bnstw.com;
    return 404; # managed by Certbot
}
   
6. **启动后端服务**'uvicorn backend.main：app --reload --host 0.0.0.0 --port 8000'后端 API 将在 'http://localhost:8000' 可用

7. **启动前端**打开 VSCode 并导航到“frontend/”目录

8. 右键单击“index.html”并选择“使用 Live Server 打开”

9. 在“http://localhost:5500”处访问前端

10.  **刷新 ESP32 固件**请参阅详细指南：“firmware/esp32/README.md”

## 📂 目录结构

backend/ # 后端核心（API、模型、服务）
  main.py # FastAPI 入口点
  routers/ # 模块路线（失语症、肢体训练、用户）
  api/ # 业务数据的 CRUD 接口
  aphasia/ # 语音分析模块
  models/ # 数据模型 （Pydantic）
  services/ # 业务逻辑 & AI 分析
  ml_models/ # 预训练的 AI 模型
  data/ # 训练/测试数据集

frontend/ # 前端页面和资源
  index.html # 主页
  aphasia/ # 失语症培训页面
  lower_limb/ # 下肢训练页面
  upper_limb/ # 上肢训练页面
  static/ # 脚本、样式和图像

firmware/ # ESP32/机器人固件
nginx/ # 部署配置 & SSL
requirements.txt# Python 依赖项


## 🔌 核心 API 接口

### AI分析

- “POST /speech/analyze-pronunciation” - 语音评估（音频 + 参考文本→分数 + 建议）

- 'POST /pose_data_stats' - 从视频捕获的姿势数据生成训练文件

- “POST /generate_training_plan” - 制定个性化的培训计划

### 患者管理

- 'POST /api/login' - 医生/患者登录

- 'POST /api/patients' - 查询患者列表

- 'POST /api/rehabilitation-progress/{patientId}' - 管理康复进度

完整的 API 文档：'docs/api/README'

## 🤖 硬件集成

- 支持的设备：ESP32、步进电机、运动传感器、语音模块

- 通信协议：蓝牙 4.2+、串口 （RS232）

- 固件开发：Arduino IDE + ESP32 板支持

- 指南：“firmware/documentation/communication_protocol.md”

## 📱 演示与支持

- **在线演示**：[AI康复训练平台演示]（https://bnstw.com/ai/frontend/index.html）

- **帮助中心**：参考演示网站文档或联系维护人员

- **问题跟踪**：使用 GitHub Issues 进行错误报告和功能请求

## 📱 项目未来计划
围绕 “智能化、场景化、远程化” 核心方向，分阶段迭代升级，逐步完善康复服务生态：
- **v1.1：移动端适配与优化**
          开发 iOS/Android 双端原生 App，支持手机 / 平板无缝使用
          适配移动端触控操作，优化小屏数据展示与康复动作引导
          新增离线模式，支持无网络环境下查看康复计划、记录训练数据

- **v1.2：深度传感器融合升级**
          接入红外、姿态传感器，精准捕捉肢体运动轨迹与关节角度
          实时反馈动作标准度，生成可视化运动热力图
          支持多传感器数据同步，提升康复评估的准确性与客观性

- **v2.0：医院端远程康复系统**
          搭建医生端管理后台，支持远程查看患者训练数据、评估康复进度
          新增在线问诊模块，患者可实时咨询康复疑问、获取个性化调整建议
          打通医院电子病历系统，实现康复计划与临床治疗方案联动

- **v3.0：AI 大模型康复助手**
          基于康复医学知识库，打造智能问答助手，即时解答训练疑问
          结合患者历史数据、身体状况，动态生成个性化康复方案
          新增语音交互、动作识别指导功能，降低操作门槛，提升使用便捷性

## 👥 贡献指南

1. 分叉仓库

2. 创建一个功能分支：'git checkout -b feature/your-feature'

3. 遵循编码约定：英文标识符、snake_case命名

4. 提交更改：'git commit -m “添加您的功能”'

5. 推送到分支：“git push origin feature/your-feature”

6. 提交拉取请求

## ⚠️ 常见问题

- ❌ 不要将大文件（模型、数据集、日志）上传到 GitHub

- 🔒 妥善处理 SSL 证书和敏感数据

- 📝 推荐的 .gitignore 条目：'.venv/、__pycache__/、logs/、saved_models/'

- ❌ 部分设备浏览器不支持MediaPipe

- ❌ 语音识别在嘈杂环境准确率下降

- ❌ ESP32 蓝牙延迟问题

- ❌ 模型推理时间偏长

## 🔒 安全与隐私

- 患者数据无须上传公网服务器，相关AI大模型本地化部署

- 本系统支持本地部署

## 📄 许可证

该项目根据 MIT 许可证获得许可 - 有关详细信息，请参阅 [LICENSE]（请将 LICENSE 文件添加到您的存储库）。

## 🧑💻 作者 & 隶属关系

- 作者：凌音

- 隶属关系：中国人民大学附属高中



该项目根据 MIT 许可证获得许可 - 有关详细信息，请参阅 [LICENSE]
