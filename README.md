# Mengangchengnline.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>梦羊城</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        
        body {
            background-color: #000;
            color: #ff6600;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }
        
        .scan-line {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #ff6600, transparent);
            z-index: 3;
            animation: scan 5s linear infinite;
            opacity: 0.3;
            pointer-events: none;
        }
        
        @keyframes scan {
            0% { top: 0; }
            100% { top: 100%; }
        }
        
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background-color: #000;
            z-index: 10;
        }
        
        .title-container {
            text-align: center;
            margin-bottom: 50px;
        }
        
        .main-title {
            font-size: 3.5rem;
            font-weight: 300;
            letter-spacing: 8px;
            margin-bottom: 15px;
            color: #ff6600;
            position: relative;
        }
        
        .main-title::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 1px;
            background: linear-gradient(90deg, transparent, #ff6600, transparent);
            animation: lineAppear 1s forwards;
            animation-delay: 0.5s;
            opacity: 0;
        }
        
        @keyframes lineAppear {
            to { opacity: 1; }
        }
        
        .subtitle {
            font-size: 1.2rem;
            letter-spacing: 3px;
            color: #cc5500;
            margin-top: 10px;
        }
        
        .loading-container {
            width: 80%;
            max-width: 600px;
            margin-bottom: 30px;
        }
        
        .loading-text {
            font-size: 1.2rem;
            text-align: center;
            margin-bottom: 20px;
            height: 24px;
            color: #ff6600;
            letter-spacing: 1px;
        }
        
        .loading-bar-container {
            width: 100%;
            height: 30px;
            background-color: #000;
            border: 2px solid #ff6600;
            position: relative;
            overflow: hidden;
        }
        
        .loading-bar {
            position: absolute;
            top: 0;
            left: 0;
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #cc4400, #ff6600, #cc4400);
            transition: width 0.2s ease;
        }
        
        .percentage {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #fff;
            font-weight: bold;
            text-shadow: 0 0 5px #000;
            z-index: 2;
        }
        
        .final-message {
            font-size: 1.5rem;
            letter-spacing: 3px;
            margin: 30px 0;
            color: #ff6600;
            opacity: 0;
            transition: opacity 1s;
            position: relative;
            padding: 10px 20px;
            background: rgba(0, 0, 0, 0.7);
            border: 1px solid rgba(255, 102, 0, 0.3);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .noise-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(255, 102, 0, 0.1) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 102, 0, 0.1) 1px, transparent 1px);
            background-size: 3px 3px;
            opacity: 0.3;
            animation: noiseFlicker 0.5s infinite alternate;
        }
        
        @keyframes noiseFlicker {
            0% { opacity: 0.2; }
            100% { opacity: 0.4; }
        }
        
        .final-message-text {
            position: relative;
            z-index: 2;
            color: #ff6600;
            text-shadow: 0 0 3px rgba(255, 102, 0, 0.5);
        }
        
        .menu-button {
            background: none;
            border: 1px solid #ff6600;
            color: #ff6600;
            padding: 12px 30px;
            font-size: 1.1rem;
            letter-spacing: 2px;
            cursor: pointer;
            transition: all 0.3s;
            opacity: 0;
            margin-top: 20px;
            position: relative;
            z-index: 4;
        }
        
        .menu-button:hover {
            background-color: #ff6600;
            color: #000;
        }
        
        .menu-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            z-index: 5;
            display: none;
            flex-direction: column;
            overflow-y: auto;
        }
        
        .database-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            z-index: 5;
            display: none;
            flex-direction: column;
            overflow-y: auto;
        }
        
        .map-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            z-index: 5;
            display: none;
            flex-direction: column;
            overflow-y: auto;
        }
        
        .menu-header {
            text-align: center;
            padding: 40px 20px 20px;
            background-color: rgba(0, 0, 0, 0.9);
            position: sticky;
            top: 0;
            z-index: 20;
            border-bottom: 1px solid #333;
        }
        
        .menu-title {
            font-size: 2.5rem;
            font-weight: 300;
            letter-spacing: 5px;
            color: #ff6600;
            margin-bottom: 10px;
        }
        
        .menu-subtitle {
            font-size: 1rem;
            color: #cc5500;
            letter-spacing: 2px;
        }
        
        .menu-content {
            max-width: 900px;
            width: 100%;
            margin: 0 auto;
            padding: 20px;
            padding-bottom: 80px;
        }
        
        .menu-section {
            margin-bottom: 15px;
            border: 1px solid #333;
            background-color: rgba(20, 10, 0, 0.3);
            transition: all 0.3s;
        }
        
        .menu-section:hover {
            border-color: #ff6600;
        }
        
        .section-header {
            padding: 15px 20px;
            font-size: 1.3rem;
            color: #ff6600;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }
        
        .section-header:hover {
            background-color: rgba(255, 102, 0, 0.1);
        }
        
        .section-header::after {
            content: '+';
            font-size: 1.5rem;
            transition: transform 0.3s;
        }
        
        .section-header.active::after {
            content: '-';
        }
        
        /* 新增：频繁点击报错效果 */
        .section-header.error-effect {
            animation: errorFlash 0.5s ease;
            color: #ff0000 !important;
            border-color: #ff0000 !important;
        }
        
        @keyframes errorFlash {
            0% {
                background-color: rgba(255, 0, 0, 0.1);
                color: #ff0000;
            }
            50% {
                background-color: rgba(255, 0, 0, 0.3);
                color: #ff0000;
            }
            100% {
                background-color: rgba(255, 102, 0, 0.1);
                color: #ff6600;
            }
        }
        
        .section-content {
            padding: 0;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s, padding 0.5s;
            background-color: rgba(30, 15, 0, 0.2);
        }
        
        .section-content.active {
            padding: 0;
            max-height: 2000px;
        }
        
        .timescreen-content-item {
            padding: 0;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s, padding 0.5s;
            background-color: rgba(30, 15, 0, 0.2);
        }
        
        .timescreen-content-item.active {
            padding: 20px;
            max-height: 2000px;
        }
        
        .timescreen-article {
            padding: 25px;
            border-bottom: 1px solid rgba(255, 102, 0, 0.1);
        }
        
        .timescreen-article:last-child {
            border-bottom: none;
        }
        
        .article-title {
            font-size: 1.4rem;
            color: #ff6600;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .article-date {
            font-size: 0.9rem;
            color: #cc5500;
            background-color: rgba(255, 102, 0, 0.1);
            padding: 3px 10px;
            border-radius: 3px;
        }
        
        .article-content {
            color: #ff8844;
            line-height: 1.6;
            font-size: 1rem;
            margin-top: 15px;
            position: relative;
            padding: 5px;
        }
        
        .article-content:hover {
            background-color: rgba(255, 102, 0, 0.05);
        }
        
        .editable-text {
            cursor: pointer;
            transition: all 0.3s;
            padding: 2px 4px;
            border-radius: 2px;
        }
        
        .editable-text:hover {
            background-color: rgba(255, 102, 0, 0.1);
            outline: 1px dashed rgba(255, 102, 0, 0.3);
        }
        
        .article-tag {
            display: inline-block;
            padding: 3px 8px;
            background-color: rgba(255, 102, 0, 0.1);
            color: #ff6600;
            font-size: 0.8rem;
            border-radius: 3px;
            margin-right: 5px;
            margin-top: 10px;
        }
        
        .submenu-section {
            margin: 0;
            border: none;
            border-top: 1px solid rgba(255, 102, 0, 0.1);
            background-color: rgba(40, 20, 0, 0.2);
        }
        
        .submenu-section:first-child {
            border-top: none;
        }
        
        .submenu-section .section-header {
            padding: 12px 20px 12px 30px;
            font-size: 1.1rem;
            background-color: rgba(30, 15, 0, 0.3);
        }
        
        .submenu-section .section-content {
            background-color: rgba(50, 25, 0, 0.3);
        }
        
        .submenu-section .section-content.active {
            padding: 0;
        }
        
        .subsubmenu-section {
            margin: 0;
            border: none;
            border-top: 1px solid rgba(255, 102, 0, 0.05);
            background-color: rgba(60, 30, 0, 0.2);
        }
        
        .subsubmenu-section .section-header {
            padding: 10px 20px 10px 40px;
            font-size: 1rem;
            background-color: rgba(40, 20, 0, 0.3);
        }
        
        .content-text {
            color: #ff8844;
            line-height: 1.6;
            font-size: 1.1rem;
            text-align: center;
            padding: 30px 20px;
            position: relative;
            z-index: 3;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .content-text:hover {
            background-color: rgba(255, 102, 0, 0.05);
        }
        
        .submenu-content-text {
            color: #ffaa66;
            line-height: 1.6;
            font-size: 1rem;
            text-align: center;
            padding: 20px;
            position: relative;
            z-index: 3;
        }
        
        .timescreen-text {
            color: #ff8844;
            line-height: 1.6;
            font-size: 1.1rem;
            padding: 20px;
            position: relative;
            z-index: 3;
        }
        
        .map-placeholder {
            color: #ff8844;
            font-size: 1.5rem;
            text-align: center;
            padding: 100px 20px;
            border: 2px dashed rgba(255, 102, 0, 0.3);
            margin: 20px;
            background-color: rgba(20, 10, 0, 0.2);
        }
        
        /* 底部按钮容器 - 改为横向分布 */
        .footer-button-container {
            display: flex;
            justify-content: center;
            gap: 15px;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.9);
            position: sticky;
            bottom: 0;
            z-index: 20;
            border-top: 1px solid #333;
            flex-direction: row; /* 明确设置为横向 */
            flex-wrap: wrap;
        }
        
        .back-button {
            background: none;
            border: 1px solid #ff6600;
            color: #ff6600;
            padding: 10px 20px;
            font-size: 0.95rem;
            letter-spacing: 1px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            z-index: 4;
            min-width: 140px;
            flex: 1;
            max-width: 180px;
        }
        
        .switch-button {
            background: none;
            border: 1px solid #ff6600;
            color: #ff6600;
            padding: 10px 20px;
            font-size: 0.95rem;
            letter-spacing: 1px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            z-index: 4;
            min-width: 140px;
            flex: 1;
            max-width: 180px;
        }
        
        .back-button:hover, .switch-button:hover {
            background-color: #ff6600;
            color: #000;
        }
        
        /* 编辑模态框样式 */
        .edit-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .edit-modal-content {
            background-color: #000;
            border: 2px solid #ff6600;
            width: 90%;
            max-width: 500px;
            padding: 20px;
            box-shadow: 0 0 20px rgba(255, 102, 0, 0.5);
        }
        
        .edit-modal-header {
            color: #ff6600;
            font-size: 1.5rem;
            margin-bottom: 15px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 102, 0, 0.3);
            padding-bottom: 10px;
        }
        
        .edit-modal-label {
            color: #ff8844;
            display: block;
            margin-bottom: 5px;
            font-size: 1rem;
        }
        
        .edit-textarea {
            width: 100%;
            height: 150px;
            background-color: rgba(20, 10, 0, 0.5);
            border: 1px solid #ff6600;
            color: #ff8844;
            padding: 10px;
            font-size: 1rem;
            resize: vertical;
            margin-bottom: 15px;
        }
        
        .edit-password-input {
            width: 100%;
            padding: 8px;
            background-color: rgba(20, 10, 0, 0.5);
            border: 1px solid #ff6600;
            color: #ff8844;
            margin-bottom: 15px;
            font-size: 1rem;
        }
        
        .edit-modal-buttons {
            display: flex;
            justify-content: space-between;
            gap: 10px;
        }
        
        .edit-modal-button {
            flex: 1;
            padding: 10px;
            background: none;
            border: 1px solid #ff6600;
            color: #ff6600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 0.95rem;
        }
        
        .edit-modal-button:hover {
            background-color: #ff6600;
            color: #000;
        }
        
        .edit-modal-button.save {
            border-color: #00ff00;
            color: #00ff00;
        }
        
        .edit-modal-button.save:hover {
            background-color: #00ff00;
            color: #000;
        }
        
        .edit-modal-button.cancel {
            border-color: #ff0000;
            color: #ff0000;
        }
        
        .edit-modal-button.cancel:hover {
            background-color: #ff0000;
            color: #000;
        }
        
        .edit-notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: rgba(0, 0, 0, 0.9);
            border: 1px solid #ff6600;
            color: #ff6600;
            padding: 10px 20px;
            z-index: 1001;
            display: none;
            box-shadow: 0 0 10px rgba(255, 102, 0, 0.5);
        }
        
        .edit-notification.success {
            border-color: #00ff00;
            color: #00ff00;
        }
        
        .edit-notification.error {
            border-color: #ff0000;
            color: #ff0000;
        }
        
        .glitch-effect {
            position: relative;
            display: inline-block;
        }
        
        .glitch-effect::before,
        .glitch-effect::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: transparent;
        }
        
        .glitch-effect::before {
            left: 2px;
            text-shadow: -2px 0 #ff0066;
            clip: rect(24px, 550px, 90px, 0);
            animation: glitch-anim-1 5s infinite linear alternate-reverse;
        }
        
        .glitch-effect::after {
            left: -2px;
            text-shadow: -2px 0 #0066ff;
            clip: rect(85px, 550px, 140px, 0);
            animation: glitch-anim-2 5s infinite linear alternate-reverse;
        }
        
        @keyframes glitch-anim-1 {
            0% { clip: rect(20px, 9999px, 25px, 0); }
            5% { clip: rect(32px, 9999px, 80px, 0); }
            10% { clip: rect(54px, 9999px, 65px, 0); }
            15% { clip: rect(12px, 9999px, 78px, 0); }
            20% { clip: rect(63px, 9999px, 89px, 0); }
            25% { clip: rect(34px, 9999px, 45px, 0); }
            30% { clip: rect(78px, 9999px, 99px, 0); }
            35% { clip: rect(62px, 9999px, 25px, 0); }
            100% { clip: rect(62px, 9999px, 25px, 0); }
        }
        
        @keyframes glitch-anim-2 {
            0% { clip: rect(85px, 9999px, 90px, 0); }
            5% { clip: rect(15px, 9999px, 30px, 0); }
            10% { clip: rect(70px, 9999px, 95px, 0); }
            15% { clip: rect(25px, 9999px, 50px, 0); }
            20% { clip: rect(5px, 9999px, 15px, 0); }
            25% { clip: rect(60px, 9999px, 75px, 0); }
            30% { clip: rect(90px, 9999px, 100px, 0); }
            35% { clip: rect(10px, 9999px, 35px, 0); }
            100% { clip: rect(10px, 9999px, 35px, 0); }
        }
        
        .status-indicator {
            position: fixed;
            top: 15px;
            right: 15px;
            background-color: rgba(255, 102, 0, 0.1);
            border: 1px solid rgba(255, 102, 0, 0.3);
            padding: 5px 10px;
            font-size: 0.8rem;
            color: #ff6600;
            z-index: 100;
        }
        
        @media (max-width: 768px) {
            .main-title {
                font-size: 2.5rem;
                letter-spacing: 5px;
            }
            
            .menu-title {
                font-size: 2rem;
            }
            
            .section-header {
                font-size: 1.1rem;
            }
            
            .final-message {
                font-size: 1.3rem;
            }
            
            .submenu-section .section-header {
                padding-left: 25px;
            }
            
            .subsubmenu-section .section-header {
                padding-left: 35px;
            }
            
            .footer-button-container {
                flex-direction: row;
                flex-wrap: wrap;
                gap: 10px;
            }
            
            .back-button, .switch-button {
                min-width: 120px;
                width: calc(33.333% - 10px);
                max-width: 160px;
                padding: 8px 12px;
                font-size: 0.85rem;
            }
        }
        
        @media (max-width: 480px) {
            .main-title {
                font-size: 2rem;
                letter-spacing: 3px;
            }
            
            .menu-title {
                font-size: 1.8rem;
            }
            
            .article-title {
                font-size: 1.2rem;
                flex-direction: column;
                align-items: flex-start;
                gap: 5px;
            }
            
            .footer-button-container {
                flex-direction: row;
                flex-wrap: wrap;
                gap: 8px;
            }
            
            .back-button, .switch-button {
                min-width: 100px;
                width: calc(50% - 8px);
                max-width: 140px;
                padding: 6px 10px;
                font-size: 0.8rem;
            }
            
            .edit-modal-content {
                width: 95%;
                padding: 15px;
            }
        }
        
        @media (max-width: 360px) {
            .footer-button-container {
                flex-direction: column;
                align-items: center;
            }
            
            .back-button, .switch-button {
                width: 100%;
                max-width: 200px;
                margin-bottom: 5px;
            }
        }
    </style>
</head>
<body>
    <!-- 扫描线效果 -->
    <div class="scan-line"></div>
    
    <!-- 状态指示器 -->
    <div class="status-indicator" id="statusIndicator">CH-AI 系统: 初始化</div>
    
    <!-- 编辑模态框 -->
    <div class="edit-modal" id="editModal">
        <div class="edit-modal-content">
            <div class="edit-modal-header">编辑内容</div>
            <label class="edit-modal-label">编辑内容:</label>
            <textarea class="edit-textarea" id="editTextarea"></textarea>
            <label class="edit-modal-label">修改密码 (20100812):</label>
            <input type="password" class="edit-password-input" id="editPasswordInput" placeholder="输入修改密码">
            <div class="edit-modal-buttons">
                <button class="edit-modal-button save" id="editSaveButton">保存</button>
                <button class="edit-modal-button cancel" id="editCancelButton">取消</button>
            </div>
        </div>
    </div>
    
    <!-- 编辑通知 -->
    <div class="edit-notification" id="editNotification"></div>
    
    <!-- 加载界面 -->
    <div class="loading-screen" id="loadingScreen">
        <div class="title-container">
            <h1 class="main-title">DREAM GOAT CITY</h1>
            <div class="subtitle">采用CH级城市管理AI技术</div>
        </div>
        
        <div class="loading-container">
            <div class="loading-text" id="loadingText">系统初始化中...</div>
            <div class="loading-bar-container">
                <div class="loading-bar" id="loadingBar"></div>
                <div class="percentage" id="percentage">0%</div>
            </div>
        </div>
        
        <div class="final-message" id="finalMessage">
            <div class="noise-overlay"></div>
            <span class="final-message-text">一切为了██</span>
        </div>
        
        <!-- 单一进入系统按钮 -->
        <button class="menu-button" id="menuButton">进入系统</button>
    </div>
        <!-- 时报界面 - 第一个界面 -->
    <div class="menu-screen" id="timescreen">
        <div class="menu-header">
            <h2 class="menu-title">梦羊城时报</h2>
            <div class="menu-subtitle">CH-AI 实时新闻系统 v2.4.1</div>
        </div>
        
        <div class="menu-content">
            <!-- 今日头条 -->
            <div class="menu-section">
                <div class="section-header" data-target="headline-news">
                    今日头条
                </div>
                <div class="section-content" id="headline-news">
                    <div class="timescreen-article">
                        <div class="article-title">
                            <span class="article-date">3025-11-23</span>
                            <span>文本</span>
                        </div>
                        <div class="article-content">
                            <p class="editable-text" data-edit-id="headline-content-1">此处应填有文本。</p>
                        </div>
                        <div>
                            <span class="article-tag">科技</span>
                            <span class="article-tag">CH-AI</span>
                            <span class="article-tag">系统升级</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 城市动态 -->
            <div class="menu-section">
                <div class="section-header" data-target="city-dynamics">
                    城市动态
                </div>
                <div class="section-content" id="city-dynamics">
                    <div class="timescreen-article">
                        <div class="article-title">
                            <span class="article-date">3025-11-22</span>
                            <span>文本</span>
                        </div>
                        <div class="article-content">
                            <p class="editable-text" data-edit-id="city-content-1">此处应填有文本。</p>
                        </div>
                        <div>
                            <span class="article-tag">农业</span>
                            <span class="article-tag">城市建设</span>
                            <span class="article-tag">可持续发展</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 科技前沿 -->
            <div class="menu-section">
                <div class="section-header" data-target="tech-frontier">
                    科技前沿
                </div>
                <div class="section-content" id="tech-frontier">
                    <div class="timescreen-article">
                        <div class="article-title">
                            <span class="article-date">3025-11-20</span>
                            <span>文本</span>
                        </div>
                        <div class="article-content">
                            <p class="editable-text" data-edit-id="tech-content-1">此处应填有文本。</p>
                        </div>
                        <div>
                            <span class="article-tag">科研</span>
                            <span class="article-tag">跨维度</span>
                            <span class="article-tag">通信技术</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 时报底部按钮 - 横向分布：数据库、地图、返回加载界面 -->
        <div class="footer-button-container">
            <button class="switch-button" id="timescreenToDatabaseButton">
                数据库
            </button>
            <button class="switch-button" id="timescreenToMapButton">
                地图
            </button>
            <button class="back-button" id="timescreenBackButton">
                返回加载界面
            </button>
        </div>
    </div>
<!-- 数据库界面 - 第二个界面 -->
<div class="database-screen" id="databaseScreen">
    <div class="menu-header">
        <h2 class="menu-title">梦羊城数据库</h2>
        <div class="menu-subtitle">CH-AI 中央档案系统 v3.7.2</div>
    </div>
    
    <div class="menu-content">
        <!-- 1. 编年史 -->
        <div class="menu-section">
            <div class="section-header" data-target="chronicles">
                编年史
            </div>
            <div class="section-content" id="chronicles">
                <div class="content-text editable-text" data-edit-id="chronicles-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 2. 公司 -->
        <div class="menu-section">
            <div class="section-header" data-target="company">
                公司
            </div>
            <div class="section-content" id="company">
                <div class="content-text editable-text" data-edit-id="company-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 3. 种族 -->
        <div class="menu-section">
            <div class="section-header" data-target="races">
                种族
            </div>
            <div class="section-content" id="races">
                <div class="content-text editable-text" data-edit-id="races-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 4. 民间组织 -->
        <div class="menu-section">
            <div class="section-header" data-target="civilian-orgs">
                民间组织
            </div>
            <div class="section-content" id="civilian-orgs">
                <div class="content-text editable-text" data-edit-id="civilian-orgs-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 5. 神秘术 -->
        <div class="menu-section">
            <div class="section-header" data-target="mysticism">
                神秘术
            </div>
            <div class="section-content" id="mysticism">
                <div class="content-text editable-text" data-edit-id="mysticism-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 6. 官方组织 -->
        <div class="menu-section">
            <div class="section-header" data-target="official-orgs">
                官方组织
            </div>
            <div class="section-content" id="official-orgs">
                <div class="content-text editable-text" data-edit-id="official-orgs-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 7. 梅林坐标系 -->
        <div class="menu-section">
            <div class="section-header" data-target="merlin-coordinates">
                梅林坐标系
            </div>
            <div class="section-content" id="merlin-coordinates">
                <div class="content-text editable-text" data-edit-id="merlin-coordinates-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 8. 政权 -->
        <div class="menu-section">
            <div class="section-header" data-target="government">
                政权
            </div>
            <div class="section-content" id="government">
                <div class="content-text editable-text" data-edit-id="government-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 9. 宗教 -->
        <div class="menu-section">
            <div class="section-header" data-target="religion">
                宗教
            </div>
            <div class="section-content" id="religion">
                <div class="content-text editable-text" data-edit-id="religion-content">
                    此处应填有文本
                </div>
            </div>
        </div>
                <!-- 10. 梦羊城市政简章 -->
        <div class="menu-section">
            <div class="section-header" data-target="city-charter">
                梦羊城市政简章
            </div>
            <div class="section-content" id="city-charter">
                <div class="content-text editable-text" data-edit-id="city-charter-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 11. 法律法规 -->
        <div class="menu-section">
            <div class="section-header" data-target="laws">
                法律法规
            </div>
            <div class="section-content" id="laws">
                <div class="content-text editable-text" data-edit-id="laws-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 12. 炼金术 -->
        <div class="menu-section">
            <div class="section-header" data-target="alchemy">
                炼金术
            </div>
            <div class="section-content" id="alchemy">
                <div class="content-text editable-text" data-edit-id="alchemy-content">
                    此处应填有文本
                </div>
            </div>
        </div>
        
        <!-- 13. 认知腐蚀抑制线 -->
        <div class="menu-section">
            <div class="section-header" data-target="cognition-suppression">
                认知腐蚀抑制线
            </div>
            <div class="section-content" id="cognition-suppression">
                <div class="content-text editable-text" data-edit-id="cognition-suppression-content">
                    此处应填有文本
                </div>
            </div>
        </div>
    </div>
    
    <!-- 数据库底部按钮 - 横向分布：时报、地图、返回加载界面 -->
    <div class="footer-button-container">
        <button class="switch-button" id="databaseToTimescreenButton">
            时报
        </button>
        <button class="switch-button" id="databaseToMapButton">
            地图
        </button>
        <button class="back-button" id="databaseBackButton">
            返回加载界面
        </button>
    </div>
</div>

<!-- 地图界面 - 第三个界面 -->
<div class="map-screen" id="mapScreen">
    <div class="menu-header">
        <h2 class="menu-title">梦羊城地图</h2>
        <div class="menu-subtitle">CH-AI 空间导航系统 v1.5.3</div>
    </div>
    
    <div class="menu-content">
        <div class="map-placeholder">
            地图系统正在开发中...
            <br>
            <br>
            梅林坐标系加载中...
            <br>
            <br>
            当前维度：Alpha-7
            <br>
            状态：稳定
        </div>
    </div>
    
    <!-- 地图底部按钮 - 横向分布：时报、数据库、返回加载界面 -->
    <div class="footer-button-container">
        <button class="switch-button" id="mapToTimescreenButton">
            时报
        </button>
        <button class="switch-button" id="mapToDatabaseButton">
            数据库
        </button>
        <button class="back-button" id="mapBackButton">
            返回加载界面
        </button>
    </div>
</div>
<script>
    // 等待DOM完全加载
    document.addEventListener('DOMContentLoaded', function() {
        console.log("DOM加载完成，开始初始化...");
        
        // 获取元素
        const loadingScreen = document.getElementById('loadingScreen');
        const timescreen = document.getElementById('timescreen');
        const databaseScreen = document.getElementById('databaseScreen');
        const mapScreen = document.getElementById('mapScreen');
        const loadingBar = document.getElementById('loadingBar');
        const percentage = document.getElementById('percentage');
        const loadingText = document.getElementById('loadingText');
        const finalMessage = document.getElementById('finalMessage');
        const menuButton = document.getElementById('menuButton');
        const statusIndicator = document.getElementById('statusIndicator');
        
        // 获取按钮元素 - 时报界面
        const timescreenBackButton = document.getElementById('timescreenBackButton');
        const timescreenToDatabaseButton = document.getElementById('timescreenToDatabaseButton');
        const timescreenToMapButton = document.getElementById('timescreenToMapButton');
        
        // 获取按钮元素 - 数据库界面
        const databaseBackButton = document.getElementById('databaseBackButton');
        const databaseToTimescreenButton = document.getElementById('databaseToTimescreenButton');
        const databaseToMapButton = document.getElementById('databaseToMapButton');
        
        // 获取按钮元素 - 地图界面
        const mapBackButton = document.getElementById('mapBackButton');
        const mapToTimescreenButton = document.getElementById('mapToTimescreenButton');
        const mapToDatabaseButton = document.getElementById('mapToDatabaseButton');
        
        // 获取编辑相关元素
        const editModal = document.getElementById('editModal');
        const editTextarea = document.getElementById('editTextarea');
        const editPasswordInput = document.getElementById('editPasswordInput');
        const editSaveButton = document.getElementById('editSaveButton');
        const editCancelButton = document.getElementById('editCancelButton');
        const editNotification = document.getElementById('editNotification');
        
        // 检查元素是否找到
        if (!loadingScreen || !timescreen || !databaseScreen || !mapScreen || !loadingBar || !percentage || !loadingText || !finalMessage || !menuButton || !statusIndicator) {
            console.error("部分元素未找到，请检查HTML结构");
            return;
        }
        
        console.log("所有元素加载成功");
        
        // 初始化元素状态
        finalMessage.style.opacity = '0';
        finalMessage.style.display = 'block';
        menuButton.style.opacity = '0';
        menuButton.style.display = 'block';
        timescreen.style.display = 'none';
        databaseScreen.style.display = 'none';
        mapScreen.style.display = 'none';
        editModal.style.display = 'none';
        editNotification.style.display = 'none';
        
        // 创建音频上下文（用于生成音效）
        let audioContext;
        let isAudioContextInitialized = false;
        let lastSoundTime = 0; // 记录上次播放音效的时间
        const SOUND_COOLDOWN = 100; // 音效冷却时间(毫秒)，避免连续播放
        
        // 初始化音频上下文
        function initAudioContext() {
            if (typeof AudioContext !== 'undefined') {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
                isAudioContextInitialized = true;
                console.log("音频上下文初始化成功");
            } else {
                console.warn("Web Audio API 不支持，音效功能不可用");
            }
        }
        
        // 检查是否可以播放音效（避免频繁播放）
        function canPlaySound() {
            const now = Date.now();
            if (now - lastSoundTime < SOUND_COOLDOWN) {
                return false;
            }
            lastSoundTime = now;
            return true;
        }
        
        // 播放键盘按键音效 - 类似机械键盘的声音
        function playKeyboardSound(type = 'click') {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                // 根据类型调整音效
                if (type === 'click') {
                    // 标准键盘点击声
                    oscillator.type = 'sine';
                    oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
                    oscillator.frequency.exponentialRampToValueAtTime(400, audioContext.currentTime + 0.08);
                    
                    gainNode.gain.setValueAtTime(0.08, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.1);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.1);
                } else if (type === 'enter') {
                    // 回车键音效
                    oscillator.type = 'sine';
                    oscillator.frequency.setValueAtTime(600, audioContext.currentTime);
                    oscillator.frequency.setValueAtTime(500, audioContext.currentTime + 0.05);
                    oscillator.frequency.setValueAtTime(400, audioContext.currentTime + 0.1);
                    
                    gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.15);
                } else if (type === 'space') {
                    // 空格键音效（更深沉）
                    oscillator.type = 'sine';
                    oscillator.frequency.setValueAtTime(200, audioContext.currentTime);
                    oscillator.frequency.exponentialRampToValueAtTime(100, audioContext.currentTime + 0.12);
                    
                    gainNode.gain.setValueAtTime(0.07, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.15);
                }
                
                console.log(`播放键盘音效: ${type}`);
            } catch (error) {
                console.error("播放键盘音效时出错:", error);
            }
        }
        
        // 播放故障音效 - 更轻、更短的电子音效
        function playGlitchSound() {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator1 = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator1.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                // 轻微的数字故障音效
                oscillator1.type = 'square';
                oscillator1.frequency.setValueAtTime(150, audioContext.currentTime);
                oscillator1.frequency.setValueAtTime(200, audioContext.currentTime + 0.02);
                oscillator1.frequency.setValueAtTime(120, audioContext.currentTime + 0.04);
                
                gainNode.gain.setValueAtTime(0.06, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.08);
                
                oscillator1.start();
                oscillator1.stop(audioContext.currentTime + 0.08);
                
                console.log("播放故障音效");
            } catch (error) {
                console.error("播放故障音效时出错:", error);
            }
        }
        
        // 播放加载界面故障音效 - 专门的加载错误音效
        function playLoadingErrorSound() {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator1 = audioContext.createOscillator();
                const oscillator2 = audioContext.createOscillator();
                const gainNode1 = audioContext.createGain();
                const gainNode2 = audioContext.createGain();
                
                // 第一个振荡器 - 低音故障
                oscillator1.connect(gainNode1);
                gainNode1.connect(audioContext.destination);
                
                oscillator1.type = 'square';
                oscillator1.frequency.setValueAtTime(80, audioContext.currentTime);
                oscillator1.frequency.setValueAtTime(60, audioContext.currentTime + 0.05);
                oscillator1.frequency.setValueAtTime(100, audioContext.currentTime + 0.1);
                
                gainNode1.gain.setValueAtTime(0.05, audioContext.currentTime);
                gainNode1.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                
                // 第二个振荡器 - 高音故障
                oscillator2.connect(gainNode2);
                gainNode2.connect(audioContext.destination);
                
                oscillator2.type = 'sawtooth';
                oscillator2.frequency.setValueAtTime(800, audioContext.currentTime);
                oscillator2.frequency.setValueAtTime(1000, audioContext.currentTime + 0.03);
                oscillator2.frequency.setValueAtTime(600, audioContext.currentTime + 0.06);
                
                gainNode2.gain.setValueAtTime(0.03, audioContext.currentTime);
                gainNode2.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.12);
                
                oscillator1.start();
                oscillator2.start();
                oscillator1.stop(audioContext.currentTime + 0.15);
                oscillator2.stop(audioContext.currentTime + 0.12);
                
                console.log("播放加载界面故障音效");
            } catch (error) {
                console.error("播放加载界面故障音效时出错:", error);
            }
        }
        
        // 播放编辑确认音效
        function playEditSound(type = 'open') {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                if (type === 'open') {
                    // 打开编辑框音效
                    oscillator.type = 'sine';
                    oscillator.frequency.setValueAtTime(400, audioContext.currentTime);
                    oscillator.frequency.setValueAtTime(600, audioContext.currentTime + 0.1);
                    
                    gainNode.gain.setValueAtTime(0.04, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.2);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.2);
                } else if (type === 'success') {
                    // 保存成功音效
                    oscillator.type = 'sine';
                    oscillator.frequency.setValueAtTime(600, audioContext.currentTime);
                    oscillator.frequency.setValueAtTime(800, audioContext.currentTime + 0.05);
                    oscillator.frequency.setValueAtTime(1000, audioContext.currentTime + 0.1);
                    
                    gainNode.gain.setValueAtTime(0.05, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.15);
                } else if (type === 'error') {
                    // 错误音效
                    oscillator.type = 'square';
                    oscillator.frequency.setValueAtTime(300, audioContext.currentTime);
                    oscillator.frequency.setValueAtTime(200, audioContext.currentTime + 0.05);
                    
                    gainNode.gain.setValueAtTime(0.06, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.1);
                    
                    oscillator.start();
                    oscillator.stop(audioContext.currentTime + 0.1);
                }
                
                console.log(`播放编辑音效: ${type}`);
            } catch (error) {
                console.error("播放编辑音效时出错:", error);
            }
        }
        
        // 播放扫描线音效 - 轻微、快速
        function playScanlineSound() {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator.type = 'sine';
                oscillator.frequency.setValueAtTime(500, audioContext.currentTime);
                oscillator.frequency.exponentialRampToValueAtTime(200, audioContext.currentTime + 0.15);
                
                gainNode.gain.setValueAtTime(0.03, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                
                oscillator.start();
                oscillator.stop(audioContext.currentTime + 0.15);
            } catch (error) {
                console.error("播放扫描线音效时出错:", error);
            }
        }
        
        // 播放数据库操作音效 - 轻微的确认音
        function playDatabaseSound() {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                // 数据库操作的轻微确认音
                oscillator.type = 'sine';
                oscillator.frequency.setValueAtTime(700, audioContext.currentTime);
                oscillator.frequency.setValueAtTime(600, audioContext.currentTime + 0.05);
                oscillator.frequency.setValueAtTime(800, audioContext.currentTime + 0.1);
                
                gainNode.gain.setValueAtTime(0.05, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
                
                oscillator.start();
                oscillator.stop(audioContext.currentTime + 0.15);
                
                console.log("播放数据库操作音效");
            } catch (error) {
                console.error("播放数据库音效时出错:", error);
            }
        }
        
        // 播放地图音效 - 轻微的空间感
        function playMapSound() {
            if (!isAudioContextInitialized || !canPlaySound()) return;
            
            try {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator.type = 'sine';
                oscillator.frequency.setValueAtTime(300, audioContext.currentTime);
                oscillator.frequency.setValueAtTime(350, audioContext.currentTime + 0.08);
                oscillator.frequency.setValueAtTime(280, audioContext.currentTime + 0.16);
                
                gainNode.gain.setValueAtTime(0.04, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.2);
                
                oscillator.start();
                oscillator.stop(audioContext.currentTime + 0.2);
                
                console.log("播放地图音效");
            } catch (error) {
                console.error("播放地图音效时出错:", error);
            }
        }
        
        // 加载阶段 - 加快加载速度
        const loadingStages = [
            { text: "正在进行精神检测", percent: 30 },
            { text: "正在进行面部扫描", percent: 60 },
            { text: "正在加固防火墙", percent: 80 },
            { text: "预加载界面", percent: 95 },
            { text: "完成安全协议", percent: 100 }
        ];
        
        let currentStage = 0;
        let currentPercent = 0;
        let isLoaded = false;
        let lastProgressUpdate = 0;
        const PROGRESS_UPDATE_INTERVAL = 20; // 加快更新频率到20ms
        
        // 记录小标题点击时间和次数
        const clickHistory = {};
        const ERROR_COOLDOWN = 300; // 错误效果冷却时间(ms)
        const RAPID_CLICK_THRESHOLD = 3; // 快速点击次数阈值
        const RAPID_CLICK_WINDOW = 1000; // 快速点击时间窗口(ms)
        
        // 编辑相关变量
        let currentEditElement = null;
        const EDIT_PASSWORD = "20100812"; // 修改密码
        
        // 更新状态指示器
        function updateStatus(text) {
            if (statusIndicator) {
                statusIndicator.textContent = `CH-AI 系统: ${text}`;
            }
        }
        
        // 随机故障效果 - 增强版，专门用于加载界面
        function triggerLoadingGlitch(element) {
            if (!element) return;
            
            const originalText = element.textContent || element.innerText;
            element.setAttribute('data-text', originalText);
            element.classList.add('glitch-effect');
            
            // 播放专门的加载界面故障音效
            playLoadingErrorSound();
            
            // 增强扫描线效果
            const scanLine = document.querySelector('.scan-line');
            if (scanLine) {
                scanLine.style.opacity = '0.8';
                scanLine.style.background = 'linear-gradient(90deg, transparent, #ff0000, transparent)';
                
                setTimeout(() => {
                    scanLine.style.opacity = '0.3';
                    scanLine.style.background = 'linear-gradient(90deg, transparent, #ff6600, transparent)';
                }, 150);
            }
            
            setTimeout(() => {
                element.classList.remove('glitch-effect');
            }, Math.random() * 400 + 300);
        }
        
        // 常规故障效果
        function triggerGlitch(element) {
            if (!element || Math.random() < 0.85) return;
            
            const originalText = element.textContent || element.innerText;
            element.setAttribute('data-text', originalText);
            element.classList.add('glitch-effect');
            
            // 播放故障音效
            playGlitchSound();
            
            setTimeout(() => {
                element.classList.remove('glitch-effect');
            }, Math.random() * 300 + 200);
        }
        
        // 随机扫描线闪烁
        function triggerScanlineFlash() {
            if (Math.random() < 0.9) return;
            
            const scanLine = document.querySelector('.scan-line');
            if (scanLine) {
                scanLine.style.opacity = '0.6';
                
                // 播放扫描线音效
                playScanlineSound();
                
                setTimeout(() => {
                    scanLine.style.opacity = '0.3';
                }, 80);
            }
        }
        
        // 触发频繁点击报错效果
        function triggerErrorEffect(element) {
            if (!element) return;
            
            // 添加报错效果类
            element.classList.add('error-effect');
            
            // 播放故障音效
            playGlitchSound();
            
            // 更新状态指示器为错误状态
            const originalStatus = statusIndicator.textContent;
            statusIndicator.textContent = "警告: 频繁操作检测";
            statusIndicator.style.color = '#ff0000';
            
            // 0.5秒后恢复
            setTimeout(() => {
                element.classList.remove('error-effect');
                statusIndicator.textContent = originalStatus;
                statusIndicator.style.color = '#ff6600';
            }, 500);
            
            console.log("触发频繁点击报错效果");
        }
        
        // 检查是否为频繁点击
        function checkRapidClick(targetId) {
            const now = Date.now();
            
            // 初始化或重置点击历史
            if (!clickHistory[targetId]) {
                clickHistory[targetId] = {
                    count: 0,
                    firstClick: now,
                    lastClick: now
                };
            }
            
            const history = clickHistory[targetId];
            
            // 如果在时间窗口内
            if (now - history.firstClick <= RAPID_CLICK_WINDOW) {
                history.count++;
                history.lastClick = now;
                
                // 如果点击次数超过阈值
                if (history.count >= RAPID_CLICK_THRESHOLD) {
                    // 重置计数
                    clickHistory[targetId] = {
                        count: 1,
                        firstClick: now,
                        lastClick: now
                    };
                    return true;
                }
            } else {
                // 重置计数
                clickHistory[targetId] = {
                    count: 1,
                    firstClick: now,
                    lastClick: now
                };
            }
            
            return false;
        }
        
        // 显示编辑通知
        function showEditNotification(message, type = 'info') {
            if (!editNotification) return;
            
            editNotification.textContent = message;
            editNotification.className = 'edit-notification';
            editNotification.classList.add(type);
            editNotification.style.display = 'block';
            
            // 播放音效
            if (type === 'success') {
                playEditSound('success');
            } else if (type === 'error') {
                playEditSound('error');
            }
            
            // 3秒后隐藏
            setTimeout(() => {
                editNotification.style.display = 'none';
            }, 3000);
        }
        
        // 打开编辑模态框
        function openEditModal(element) {
            if (!element || !editModal || !editTextarea) return;
            
            currentEditElement = element;
            editTextarea.value = element.textContent;
            editPasswordInput.value = '';
            editModal.style.display = 'flex';
            
            // 播放打开编辑框音效
            playEditSound('open');
            
            console.log("打开编辑模态框");
        }
        
        // 关闭编辑模态框
        function closeEditModal() {
            if (!editModal) return;
            
            editModal.style.display = 'none';
            currentEditElement = null;
            editTextarea.value = '';
            editPasswordInput.value = '';
            
            console.log("关闭编辑模态框");
        }
        
        // 保存编辑内容
        function saveEditContent() {
            if (!currentEditElement || !editTextarea || !editPasswordInput) return;
            
            const newText = editTextarea.value.trim();
            const password = editPasswordInput.value.trim();
            
            // 检查密码
            if (password !== EDIT_PASSWORD) {
                showEditNotification("密码错误！修改密码为: 20100812", 'error');
                return;
            }
            
            // 更新文本内容
            currentEditElement.textContent = newText;
            
            // 显示成功通知
            showEditNotification("内容修改成功！", 'success');
            
            // 关闭模态框
            closeEditModal();
            
            // 触发故障效果
            triggerGlitch(currentEditElement);
            
            console.log("保存编辑内容");
        }
        
        // 初始化编辑功能
        function initEditFunctionality() {
            console.log("初始化编辑功能...");
            
            // 为所有可编辑文本添加点击事件
            document.addEventListener('click', function(event) {
                const editableElement = event.target.closest('.editable-text');
                if (editableElement && editModal.style.display === 'none') {
                    openEditModal(editableElement);
                    event.stopPropagation();
                }
            });
            
            // 绑定保存按钮事件
            if (editSaveButton) {
                editSaveButton.addEventListener('click', saveEditContent);
            }
            
            // 绑定取消按钮事件
            if (editCancelButton) {
                editCancelButton.addEventListener('click', closeEditModal);
            }
            
            // 点击模态框外部关闭
            editModal.addEventListener('click', function(event) {
                if (event.target === editModal) {
                    closeEditModal();
                }
            });
            
            // 回车键保存，ESC键取消
            document.addEventListener('keydown', function(event) {
                if (editModal.style.display === 'flex') {
                    if (event.key === 'Enter' && (event.ctrlKey || event.metaKey)) {
                        saveEditContent();
                    } else if (event.key === 'Escape') {
                        closeEditModal();
                    }
                }
            });
            
            console.log("编辑功能初始化完成");
        }
        
        // 更新进度条 - 加快加载速度，加入更多错误特效
        function updateProgressBar(targetPercent) {
            if (isLoaded) return;
            
            const increment = 2; // 加快增量到2%
            const interval = PROGRESS_UPDATE_INTERVAL;
            
            const step = () => {
                const now = Date.now();
                if (now - lastProgressUpdate < PROGRESS_UPDATE_INTERVAL) {
                    setTimeout(step, PROGRESS_UPDATE_INTERVAL);
                    return;
                }
                
                lastProgressUpdate = now;
                
                if (currentPercent < targetPercent) {
                    currentPercent += increment;
                    if (currentPercent > targetPercent) {
                        currentPercent = targetPercent;
                    }
                    
                    if (loadingBar) {
                        loadingBar.style.width = currentPercent + '%';
                    }
                    
                    if (percentage) {
                        percentage.textContent = Math.round(currentPercent) + '%';
                    }
                    
                    // 加载界面错误特效 - 更频繁的触发
                    if (Math.random() < 0.15 && loadingText) { // 增加触发概率
                        triggerLoadingGlitch(loadingText);
                        
                        // 偶尔也触发标题的故障效果
                        if (Math.random() < 0.3) {
                            const title = document.querySelector('.main-title');
                            triggerLoadingGlitch(title);
                        }
                    }
                    
                    // 偶尔触发扫描线闪烁
                    if (Math.random() < 0.1) {
                        triggerScanlineFlash();
                    }
                    
                    // 当进度到特定阶段时触发额外故障
                    if (currentPercent > 30 && currentPercent < 35 && Math.random() < 0.5) {
                        const subtitle = document.querySelector('.subtitle');
                        triggerLoadingGlitch(subtitle);
                    }
                    
                    if (currentPercent > 70 && currentPercent < 75 && Math.random() < 0.5) {
                        const percentageText = document.getElementById('percentage');
                        triggerLoadingGlitch(percentageText);
                    }
                    
                    setTimeout(step, interval);
                } else {
                    if (currentStage < loadingStages.length - 1) {
                        currentStage++;
                        
                        // 阶段切换时触发故障效果
                        if (Math.random() < 0.7) {
                            const loadingTextElement = document.getElementById('loadingText');
                            if (loadingTextElement) {
                                triggerLoadingGlitch(loadingTextElement);
                            }
                        }
                        
                        setTimeout(() => {
                            if (loadingText) {
                                loadingText.textContent = loadingStages[currentStage].text;
                            }
                            updateProgressBar(loadingStages[currentStage].percent);
                        }, 200); // 缩短阶段切换延迟
                    } else {
                        finishLoading();
                    }
                }
            };
            
            step();
        }
                // 完成加载
        function finishLoading() {
            isLoaded = true;
            console.log("加载完成");
            
            if (loadingText) {
                loadingText.textContent = "系统就绪";
            }
            updateStatus("就绪");
            
            // 加载完成时触发一次强烈故障效果
            setTimeout(() => {
                const title = document.querySelector('.main-title');
                const subtitle = document.querySelector('.subtitle');
                const loadingTextElement = document.getElementById('loadingText');
                
                if (title) triggerLoadingGlitch(title);
                if (subtitle) triggerLoadingGlitch(subtitle);
                if (loadingTextElement) triggerLoadingGlitch(loadingTextElement);
                
                // 扫描线强烈闪烁
                const scanLine = document.querySelector('.scan-line');
                if (scanLine) {
                    for (let i = 0; i < 3; i++) {
                        setTimeout(() => {
                            scanLine.style.opacity = '0.9';
                            scanLine.style.background = 'linear-gradient(90deg, transparent, #00ff00, transparent)';
                            playScanlineSound();
                            
                            setTimeout(() => {
                                scanLine.style.opacity = '0.3';
                                scanLine.style.background = 'linear-gradient(90deg, transparent, #ff6600, transparent)';
                            }, 50);
                        }, i * 200);
                    }
                }
            }, 100);
            
            setTimeout(() => {
                if (finalMessage) {
                    finalMessage.style.opacity = '1';
                    
                    // 最终消息出现时触发故障效果
                    setTimeout(() => {
                        triggerLoadingGlitch(finalMessage.querySelector('.final-message-text'));
                    }, 300);
                }
                updateStatus("一切为了██");
                
                // 增强噪点效果
                const noiseOverlay = finalMessage.querySelector('.noise-overlay');
                if (noiseOverlay) {
                    // 增加噪点强度
                    noiseOverlay.style.opacity = '0.5';
                    noiseOverlay.style.backgroundSize = '2px 2px';
                    
                    // 添加额外的闪烁效果
                    setInterval(() => {
                        if (Math.random() < 0.5) {
                            noiseOverlay.style.opacity = (0.3 + Math.random() * 0.2) + '';
                        }
                    }, 500);
                }
                
                setTimeout(() => {
                    if (menuButton) {
                        menuButton.style.opacity = '1';
                        
                        // 按钮出现时轻微闪烁
                        menuButton.style.animation = 'pulse 2s infinite';
                        const style = document.createElement('style');
                        style.textContent = `
                            @keyframes pulse {
                                0% { opacity: 0.7; }
                                50% { opacity: 1; }
                                100% { opacity: 0.7; }
                            }
                        `;
                        document.head.appendChild(style);
                    }
                }, 300); // 缩短按钮显示延迟
            }, 300); // 缩短最终消息显示延迟
        }
        
        // 打开时报（第一个界面）
        function openTimescreen() {
            console.log("打开时报");
            playKeyboardSound('enter');
            
            const title = document.querySelector('.main-title');
            triggerGlitch(title);
            updateStatus("访问时报");
            
            setTimeout(() => {
                if (loadingScreen) {
                    loadingScreen.style.display = 'none';
                }
                
                if (databaseScreen) {
                    databaseScreen.style.display = 'none';
                }
                
                if (mapScreen) {
                    mapScreen.style.display = 'none';
                }
                
                if (timescreen) {
                    timescreen.style.display = 'flex';
                    timescreen.scrollTop = 0;
                }
            }, 300); // 缩短切换延迟
        }
        
        // 打开数据库（第二个界面）
        function openDatabase() {
            console.log("打开数据库");
            playDatabaseSound();
            
            const menuTitle = document.querySelector('.menu-title');
            triggerGlitch(menuTitle);
            updateStatus("访问数据库");
            
            setTimeout(() => {
                if (loadingScreen) {
                    loadingScreen.style.display = 'none';
                }
                
                if (timescreen) {
                    timescreen.style.display = 'none';
                }
                
                if (mapScreen) {
                    mapScreen.style.display = 'none';
                }
                
                if (databaseScreen) {
                    databaseScreen.style.display = 'flex';
                    databaseScreen.scrollTop = 0;
                }
            }, 300);
        }
        
        // 打开地图（第三个界面）
        function openMap() {
            console.log("打开地图");
            playMapSound();
            
            const menuTitle = document.querySelector('.menu-title');
            triggerGlitch(menuTitle);
            updateStatus("访问地图");
            
            setTimeout(() => {
                if (loadingScreen) {
                    loadingScreen.style.display = 'none';
                }
                
                if (timescreen) {
                    timescreen.style.display = 'none';
                }
                
                if (databaseScreen) {
                    databaseScreen.style.display = 'none';
                }
                
                if (mapScreen) {
                    mapScreen.style.display = 'flex';
                    mapScreen.scrollTop = 0;
                }
            }, 300);
        }
        
        // 关闭菜单返回加载界面
        function closeToLoading() {
            console.log("返回加载界面");
            playKeyboardSound('space');
            
            const currentTitle = document.querySelector('.menu-title');
            triggerGlitch(currentTitle);
            updateStatus("返回加载界面");
            
            setTimeout(() => {
                if (timescreen) {
                    timescreen.style.display = 'none';
                }
                
                if (databaseScreen) {
                    databaseScreen.style.display = 'none';
                }
                
                if (mapScreen) {
                    mapScreen.style.display = 'none';
                }
                
                if (loadingScreen) {
                    loadingScreen.style.display = 'flex';
                }
            }, 300);
        }
        
        // 切换菜单项 - 添加频繁点击检测
        function toggleMenuItem(targetId, header) {
            console.log("切换菜单项:", targetId);
            
            // 检查是否为频繁点击
            if (checkRapidClick(targetId)) {
                triggerErrorEffect(header);
                return;
            }
            
            playKeyboardSound('click');
            
            const content = document.getElementById(targetId);
            if (!content) {
                console.error("未找到内容元素:", targetId);
                return;
            }
            
            const isActive = content.classList.contains('active');
            
            if (isActive) {
                content.classList.remove('active');
                header.classList.remove('active');
            } else {
                content.classList.add('active');
                header.classList.add('active');
                
                // 更新状态指示器
                const menuText = header.textContent.trim();
                updateStatus(`访问: ${menuText}`);
                
                // 添加故障效果
                triggerGlitch(header);
            }
        }
        
        // 绑定菜单点击事件
        function setupMenuEvents() {
            console.log("设置菜单事件");
            
            // 绑定进入系统按钮
            if (menuButton) {
                menuButton.addEventListener('click', openTimescreen);
            }
            
            // 绑定时报界面按钮
            if (timescreenBackButton) {
                timescreenBackButton.addEventListener('click', closeToLoading);
            }
            if (timescreenToDatabaseButton) {
                timescreenToDatabaseButton.addEventListener('click', openDatabase);
            }
            if (timescreenToMapButton) {
                timescreenToMapButton.addEventListener('click', openMap);
            }
            
            // 绑定数据库界面按钮
            if (databaseBackButton) {
                databaseBackButton.addEventListener('click', closeToLoading);
            }
            if (databaseToTimescreenButton) {
                databaseToTimescreenButton.addEventListener('click', openTimescreen);
            }
            if (databaseToMapButton) {
                databaseToMapButton.addEventListener('click', openMap);
            }
            
            // 绑定地图界面按钮
            if (mapBackButton) {
                mapBackButton.addEventListener('click', closeToLoading);
            }
            if (mapToTimescreenButton) {
                mapToTimescreenButton.addEventListener('click', openTimescreen);
            }
            if (mapToDatabaseButton) {
                mapToDatabaseButton.addEventListener('click', openDatabase);
            }
            
            // 为所有菜单项添加点击事件（使用事件委托）
            document.addEventListener('click', function(event) {
                const headerElement = event.target.closest('.section-header');
                if (headerElement && headerElement.hasAttribute('data-target')) {
                    const targetId = headerElement.getAttribute('data-target');
                    toggleMenuItem(targetId, headerElement);
                }
            });
            
            console.log("菜单事件设置完成");
        }
        
        // 键盘快捷键
        function setupKeyboardShortcuts() {
            document.addEventListener('keydown', function(e) {
                // ESC键返回加载界面
                if (e.key === 'Escape' && (timescreen.style.display === 'flex' || databaseScreen.style.display === 'flex' || mapScreen.style.display === 'flex')) {
                    closeToLoading();
                }
                
                // M键打开时报（如果在加载界面）
                if (e.key === 'm' && loadingScreen.style.display !== 'none' && menuButton.style.opacity === '1') {
                    openTimescreen();
                }
                
                // 空格键加速加载（测试用）
                if (e.key === ' ' && !isLoaded) {
                    currentPercent = 100;
                    if (loadingBar) {
                        loadingBar.style.width = '100%';
                    }
                    if (percentage) {
                        percentage.textContent = '100%';
                    }
                    finishLoading();
                }
                
                // 数字键快速导航到时报菜单项
                if (timescreen.style.display === 'flex') {
                    const timescreenItems = document.querySelectorAll('.timescreen .section-header');
                    let index = -1;
                    
                    if (e.key === '1') index = 0;
                    else if (e.key === '2') index = 1;
                    else if (e.key === '3') index = 2;
                    
                    if (index >= 0 && index < timescreenItems.length) {
                        const targetId = timescreenItems[index].getAttribute('data-target');
                        if (targetId) {
                            toggleMenuItem(targetId, timescreenItems[index]);
                            
                            // 滚动到该菜单项
                            setTimeout(() => {
                                timescreenItems[index].scrollIntoView({ behavior: 'smooth', block: 'start' });
                            }, 100);
                        }
                    }
                    
                    // D键切换到数据库
                    if (e.key === 'd') {
                        openDatabase();
                    }
                    // M键切换到地图
                    if (e.key === 'm') {
                        openMap();
                    }
                }
                
                // 数字键快速导航到数据库主菜单项
                if (databaseScreen.style.display === 'flex') {
                    const menuItems = document.querySelectorAll('.database-screen .menu-section .section-header');
                    let index = -1;
                    
                    if (e.key === '1') index = 0;
                    else if (e.key === '2') index = 1;
                    else if (e.key === '3') index = 2;
                    else if (e.key === '4') index = 3;
                    else if (e.key === '5') index = 4;
                    else if (e.key === '6') index = 5;
                    else if (e.key === '7') index = 6;
                    else if (e.key === '8') index = 7;
                    else if (e.key === '9') index = 8;
                    
                    if (index >= 0 && index < menuItems.length) {
                        const targetId = menuItems[index].getAttribute('data-target');
                        if (targetId) {
                            toggleMenuItem(targetId, menuItems[index]);
                            
                            // 滚动到该菜单项
                            setTimeout(() => {
                                menuItems[index].scrollIntoView({ behavior: 'smooth', block: 'start' });
                            }, 100);
                        }
                    }
                    
                    // T键切换到时报
                    if (e.key === 't') {
                        openTimescreen();
                    }
                    // M键切换到地图
                    if (e.key === 'm') {
                        openMap();
                    }
                }
                
                // 地图界面快捷键
                if (mapScreen.style.display === 'flex') {
                    // T键切换到时报
                    if (e.key === 't') {
                        openTimescreen();
                    }
                    // D键切换到数据库
                    if (e.key === 'd') {
                        openDatabase();
                    }
                }
            });
        }
        
        // 启动加载过程
        function startLoading() {
            console.log("开始加载过程");
            
            // 初始化时立即触发一次故障效果
            setTimeout(() => {
                const title = document.querySelector('.main-title');
                const subtitle = document.querySelector('.subtitle');
                if (title) triggerLoadingGlitch(title);
                if (subtitle) triggerLoadingGlitch(subtitle);
            }, 500);
            
            setTimeout(() => {
                if (loadingText) {
                    loadingText.textContent = loadingStages[0].text;
                }
                updateProgressBar(loadingStages[0].percent);
            }, 800); // 缩短开始加载延迟
        }
        
        // 随机全局故障效果
        function setupRandomEffects() {
            // 加载界面的随机故障效果
            const loadingInterval = setInterval(() => {
                if (loadingScreen.style.display !== 'none' && !isLoaded) {
                    if (Math.random() < 0.3) { // 加载界面更高频率的故障
                        const elements = [
                            document.querySelector('.main-title'),
                            document.querySelector('.subtitle'),
                            loadingText,
                            statusIndicator
                        ].filter(el => el && el.offsetParent !== null);
                        
                        if (elements.length > 0) {
                            const randomElement = elements[Math.floor(Math.random() * elements.length)];
                            triggerLoadingGlitch(randomElement);
                        }
                    }
                } else {
                    clearInterval(loadingInterval);
                }
            }, 3000);
            
            // 其他界面的随机故障效果
            setInterval(() => {
                if (Math.random() < 0.2) {
                    const elements = [
                        document.querySelector('.main-title'),
                        document.querySelector('.menu-title'),
                        loadingText,
                        statusIndicator
                    ].filter(el => el && el.style.display !== 'none' && el.offsetParent !== null);
                    
                    if (elements.length > 0) {
                        const randomElement = elements[Math.floor(Math.random() * elements.length)];
                        triggerGlitch(randomElement);
                    }
                }
            }, 5000);
        }
        
        // 初始化所有设置
        function initialize() {
            console.log("初始化系统...");
            
            // 初始化音频上下文
            initAudioContext();
            
            // 初始化编辑功能
            initEditFunctionality();
            
            setupMenuEvents();
            setupKeyboardShortcuts();
            startLoading();
            setupRandomEffects();
            updateStatus("初始化");
            console.log("系统初始化完成");
        }
        
        // 开始初始化
        initialize();
    });
</script>
</body>
</html>
