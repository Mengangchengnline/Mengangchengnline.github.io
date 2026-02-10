# Mengangchengnline.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>梦羊城 | DREAM GOAT CITY</title>
    
    <!-- 字体 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700;800&family=Rajdhani:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background-color: #000;
            color: #ff6600;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            font-family: 'Rajdhani', sans-serif;
            user-select: none;
        }
        
        /* 视觉层 */
        .ambient-light {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
            background: radial-gradient(circle at 20% 30%, rgba(255, 102, 0, 0.15) 0%, transparent 50%),
                        radial-gradient(circle at 80% 70%, rgba(255, 102, 0, 0.1) 0%, transparent 50%);
            animation: ambientFloat 20s ease-in-out infinite alternate;
        }
        
        @keyframes ambientFloat {
            0% { transform: translate(0, 0); }
            50% { transform: translate(-2%, -1%); }
            100% { transform: translate(2%, 1%); }
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
            font-weight: 600;
            letter-spacing: 12px;
            margin-bottom: 15px;
            color: #ff6600;
            position: relative;
            height: 80px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
        }
        
        .main-title::before, .main-title::after {
            content: '';
            position: absolute;
            top: 50%;
            width: 10px;
            height: 10px;
            background: #ff6600;
            border-radius: 50%;
            transform: translateY(-50%);
            animation: titleDot 2s infinite;
        }
        
        .main-title::before {
            left: -20px;
        }
        
        .main-title::after {
            right: -20px;
            animation-delay: 0.5s;
        }
        
        @keyframes titleDot {
            0%, 100% {
                opacity: 0.3;
                transform: translateY(-50%) scale(0.8);
            }
            50% {
                opacity: 1;
                transform: translateY(-50%) scale(1.2);
            }
        }
        
        /* 标题字母效果 */
        .title-letter {
            display: inline-block;
            opacity: 0;
            transform: translateY(20px) rotateX(90deg);
            transition: opacity 0.3s, transform 0.3s;
            position: relative;
        }
        
        .title-letter.visible {
            opacity: 1;
            transform: translateY(0) rotateX(0);
        }
        
        .neon-glow {
            position: relative;
            text-shadow: 
                0 0 5px rgba(255, 102, 0, 0.7),
                0 0 10px rgba(255, 102, 0, 0.5),
                0 0 15px rgba(255, 102, 0, 0.3);
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
            min-height: 30px;
        }
        
        .loading-bar-container {
            width: 100%;
            height: 30px;
            background-color: #000;
            border: 2px solid #ff6600;
            position: relative;
            overflow: hidden;
            box-shadow: 
                0 0 20px rgba(255, 102, 0, 0.3),
                inset 0 0 10px rgba(0, 0, 0, 0.5);
        }
        
        .loading-bar {
            position: absolute;
            top: 0;
            left: 0;
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, 
                transparent 0%, 
                rgba(255, 102, 0, 0.8) 20%, 
                rgba(255, 102, 0, 1) 50%, 
                rgba(255, 102, 0, 0.8) 80%, 
                transparent 100%);
            transition: width 0.2s ease;
            animation: pulseGlow 2s infinite alternate;
        }
        
        @keyframes pulseGlow {
            0% { box-shadow: 0 0 10px rgba(255, 102, 0, 0.5); }
            100% { box-shadow: 0 0 20px rgba(255, 102, 0, 0.8); }
        }
        
        /* 百分比文字颜色保持黑色 */
        .percentage {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #000000; /* 保持黑色 */
            font-weight: bold;
            text-shadow: 0 0 2px rgba(255, 255, 255, 0.5);
            z-index: 2;
            font-size: 1rem;
            font-family: 'Orbitron', sans-serif;
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
            background-size: 50px 50px;
            opacity: 0.3;
            animation: noiseFlicker 0.5s infinite alternate, noiseMove 20s linear infinite;
        }
        
        @keyframes noiseFlicker {
            0% { opacity: 0.2; }
            100% { opacity: 0.4; }
        }
        
        @keyframes noiseMove {
            0% { background-position: 0 0; }
            100% { background-position: 100px 100px; }
        }
        
        .final-message-text {
            position: relative;
            z-index: 2;
            color: #ff6600;
            text-shadow: 0 0 3px rgba(255, 102, 0, 0.5);
        }
        /* 按钮效果 - 修复：确保按钮文字始终为橙色 */
.menu-button, .back-button, .switch-button {
    background: linear-gradient(45deg, rgba(255, 102, 0, 0.1), rgba(255, 136, 68, 0.05));
    border: 1px solid transparent;
    border-image: linear-gradient(45deg, #ff6600, #ff8844, #ff6600) 1;
    color: #ff6600 !important; /* 重要：确保按钮文字始终为橙色 */
    padding: 12px 30px;
    font-size: 1.1rem;
    letter-spacing: 2px;
    cursor: pointer;
    transition: all 0.3s ease;
    opacity: 0;
    margin-top: 20px;
    position: relative;
    z-index: 4;
    overflow: hidden;
    font-family: 'Orbitron', sans-serif;
}

.menu-button::before, .back-button::before, .switch-button::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
    transition: left 0.5s ease;
}

.menu-button:hover, .back-button:hover, .switch-button:hover {
    background-color: #ff6600;
    color: #000 !important; /* 重要：悬停时文字变为黑色 */
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(255, 102, 0, 0.3);
}

.menu-button:hover::before, .back-button:hover::before, .switch-button:hover::before {
    left: 100%;
}

.button-glow {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at center, 
        rgba(255, 102, 0, 0.3) 0%, 
        transparent 70%);
    opacity: 0;
    transition: opacity 0.3s ease;
    border-radius: inherit;
    z-index: -1;
}

.menu-button:hover .button-glow {
    opacity: 1;
    animation: buttonPulse 2s infinite;
}

@keyframes buttonPulse {
    0%, 100% {
        transform: scale(1);
        opacity: 0.3;
    }
    50% {
        transform: scale(1.1);
        opacity: 0.5;
    }
}

.button-text {
    position: relative;
    z-index: 1;
}

.menu-screen, .database-screen, .map-screen,
.company-history-screen, .company-detail-screen {
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
    backdrop-filter: blur(10px);
}

.menu-title {
    font-size: 2.5rem;
    font-weight: 600;
    letter-spacing: 5px;
    color: #ff6600;
    margin-bottom: 10px;
    font-family: 'Orbitron', sans-serif;
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
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.menu-section:hover {
    border-color: #ff6600;
    transform: translateY(-2px);
    box-shadow: 0 5px 20px rgba(255, 102, 0, 0.3);
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
    font-family: 'Orbitron', sans-serif;
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

/* 频繁点击报错效果 */
.section-header.error-effect {
    animation: errorFlash 0.5s ease;
    color: #ff0000 !important;
    border-color: #ff0000 !important;
}

@keyframes errorFlash {
    0% { background-color: rgba(255, 0, 0, 0.1); color: #ff0000; }
    50% { background-color: rgba(255, 0, 0, 0.3); color: #ff0000; }
    100% { background-color: rgba(255, 102, 0, 0.1); color: #ff6600; }
}
/* 优雅的展开动画 */
.section-content {
    padding: 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.6s cubic-bezier(0.22, 0.61, 0.36, 1), 
                padding 0.6s cubic-bezier(0.22, 0.61, 0.36, 1);
    background-color: rgba(30, 15, 0, 0.2);
}

.section-content.active {
    padding: 0;
    max-height: 2000px;
}

/* 文章卡片 */
.timescreen-article {
    padding: 25px;
    border-bottom: 1px solid rgba(255, 102, 0, 0.1);
    background: linear-gradient(135deg, 
        rgba(20, 10, 0, 0.4), 
        rgba(40, 20, 0, 0.2));
    border: 1px solid rgba(255, 102, 0, 0.3);
    border-radius: 12px;
    margin-bottom: 20px;
    transition: all 0.4s ease;
    backdrop-filter: blur(10px);
}

.timescreen-article:hover {
    border-color: #ff6600;
    box-shadow: 0 10px 30px rgba(255, 102, 0, 0.2);
    transform: translateY(-3px);
}

.article-title {
    font-size: 1.4rem;
    color: #ff6600;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 10px;
    font-family: 'Orbitron', sans-serif;
}

.article-date {
    font-size: 0.9rem;
    color: #cc5500;
    background-color: rgba(255, 102, 0, 0.1);
    padding: 3px 10px;
    border-radius: 3px;
}

.article-content {
    color: #ffaa66;
    line-height: 1.7;
    font-size: 1.05rem;
    margin-top: 15px;
    font-family: 'Rajdhani', sans-serif;
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

.content-text, .submenu-content-text, .timescreen-text {
    color: #ffaa66;
    line-height: 1.7;
    font-size: 1.1rem;
    padding: 30px 20px;
    position: relative;
    z-index: 3;
    font-family: 'Rajdhani', sans-serif;
}

.submenu-content-text {
    font-size: 1rem;
    padding: 20px;
}

.timescreen-text {
    padding: 20px;
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

/* ========== 底部导航栏 - 新增 ========== */
.bottom-navigation {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 80px;
    background-color: rgba(0, 0, 0, 0.95);
    border-top: 1px solid rgba(255, 102, 0, 0.3);
    display: flex;
    justify-content: space-around;
    align-items: center;
    z-index: 100;
    padding: 0 10px;
    backdrop-filter: blur(10px);
    transform: translateY(0);
    transition: transform 0.3s ease;
}

.bottom-navigation.hidden {
    transform: translateY(100%);
}

.nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
    flex: 1;
    max-width: 120px;
    position: relative;
    border-radius: 8px;
}

.nav-item:hover {
    background-color: rgba(255, 102, 0, 0.1);
    transform: translateY(-5px);
}

.nav-item.active {
    background-color: rgba(255, 102, 0, 0.2);
    border-bottom: 3px solid #ff6600;
}

.nav-icon {
    font-size: 1.8rem;
    margin-bottom: 5px;
    color: #ff6600;
    transition: all 0.3s ease;
}

.nav-item.active .nav-icon {
    color: #ffaa66;
    transform: scale(1.1);
    text-shadow: 0 0 10px rgba(255, 102, 0, 0.7);
}

.nav-label {
    font-size: 0.9rem;
    color: #cc5500;
    font-family: 'Rajdhani', sans-serif;
    letter-spacing: 1px;
}

.nav-item.active .nav-label {
    color: #ff6600;
    font-weight: 600;
}

/* 导航栏滑动指示器 */
.nav-slider {
    position: absolute;
    top: -10px;
    left: 50%;
    transform: translateX(-50%);
    width: 40px;
    height: 4px;
    background-color: #ff6600;
    border-radius: 2px;
    opacity: 0.6;
    cursor: grab;
    transition: opacity 0.3s ease;
}

.nav-slider:hover {
    opacity: 1;
}

/* 导航栏滑动效果区域 */
.nav-slide-area {
    position: absolute;
    top: -25px;
    left: 0;
    width: 100%;
    height: 50px;
    z-index: 101;
    cursor: grab;
}

/* 滑动指示器动画 */
@keyframes slidePulse {
    0%, 100% {
        opacity: 0.6;
    }
    50% {
        opacity: 1;
    }
}

.nav-slider.active {
    animation: slidePulse 1.5s infinite;
}

/* 导航栏底部按钮容器 */
.footer-button-container {
    display: flex;
    justify-content: center;
    gap: 15px;
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.9);
    position: sticky;
    bottom: 80px;
    z-index: 20;
    border-top: 1px solid #333;
    flex-direction: row;
    flex-wrap: wrap;
    backdrop-filter: blur(10px);
}

/* 移除原有导航指示器 */
.nav-indicator {
    display: none;
}
/* 状态指示器 */
.status-indicator {
    position: fixed;
    top: 15px;
    right: 15px;
    background: rgba(0, 0, 0, 0.6);
    border: 1px solid rgba(255, 102, 0, 0.3);
    padding: 5px 10px;
    font-size: 0.8rem;
    color: #ff6600;
    z-index: 100;
    backdrop-filter: blur(10px);
    border-radius: 20px;
    box-shadow: 0 0 15px rgba(255, 102, 0, 0.2);
    font-family: 'Orbitron', sans-serif;
}

/* 故障效果 */
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

/* 网格效果 */
.company-placeholder-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    padding: 20px;
}

@media (min-width: 768px) {
    .company-placeholder-grid {
        grid-template-columns: repeat(3, 1fr);
    }
}

.company-placeholder-item {
    background: linear-gradient(135deg, 
        rgba(255, 102, 0, 0.15), 
        rgba(255, 102, 0, 0.05));
    border: 1px solid rgba(255, 102, 0, 0.3);
    padding: 30px 15px;
    text-align: center;
    cursor: pointer;
    transition: all 0.4s ease;
    color: #ff6600;
    font-size: 1.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 120px;
    backdrop-filter: blur(5px);
    position: relative;
    overflow: hidden;
    font-family: 'Orbitron', sans-serif;
}

.company-placeholder-item::after {
    content: '';
    position: absolute;
    top: -2px;
    left: -2px;
    right: -2px;
    bottom: -2px;
    background: linear-gradient(45deg, 
        #ff6600, #ff8844, #ff6600, #ff8844);
    z-index: -1;
    border-radius: inherit;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.company-placeholder-item:hover {
    background-color: rgba(255, 102, 0, 0.2);
    border-color: #ff6600;
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 10px 20px rgba(255, 102, 0, 0.2);
}

.company-placeholder-item:hover::after {
    opacity: 1;
    animation: borderRotate 3s linear infinite;
}

@keyframes borderRotate {
    0% { background-position: 0% 50%; }
    100% { background-position: 100% 50%; }
}

/* 详情内容 */
.static-detail-content {
    padding: 30px;
    color: #ffaa66;
    line-height: 1.7;
    font-size: 1.1rem;
    background: linear-gradient(135deg, 
        rgba(20, 10, 0, 0.4), 
        rgba(40, 20, 0, 0.2));
    border: 1px solid rgba(255, 102, 0, 0.3);
    margin: 20px;
    min-height: 300px;
    backdrop-filter: blur(10px);
    border-radius: 12px;
}

/* 滚动条 */
::-webkit-scrollbar {
    width: 8px;
}

::-webkit-scrollbar-track {
    background: rgba(0, 0, 0, 0.2);
}

::-webkit-scrollbar-thumb {
    background: linear-gradient(transparent, #ff6600, transparent);
    border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
    background: linear-gradient(transparent, #ff8844, transparent);
}        /* 过渡效果 */
        .fade-in {
            animation: fadeIn 0.6s ease-out forwards;
        }
        
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* 鼠标光标 */
        .advanced-cursor {
            position: fixed;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 102, 0, 0.5);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            transition: transform 0.1s, width 0.3s, height 0.3s;
            backdrop-filter: blur(2px);
        }
        
        .advanced-cursor.hover {
            width: 40px;
            height: 40px;
            border-color: rgba(255, 102, 0, 0.8);
            background: rgba(255, 102, 0, 0.1);
        }
        
        .advanced-cursor.click {
            width: 15px;
            height: 15px;
            background: rgba(255, 102, 0, 0.3);
        }
        
        /* 页面过渡效果 */
        .page-transition {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, #000, #111, #000);
            z-index: 999;
            opacity: 0;
            pointer-events: none;
            animation: pageTransition 0.6s ease-out forwards;
        }
        
        @keyframes pageTransition {
            0% {
                opacity: 0;
                clip-path: circle(0% at 50% 50%);
            }
            50% {
                opacity: 1;
                clip-path: circle(100% at 50% 50%);
            }
            100% {
                opacity: 0;
                clip-path: circle(0% at 50% 50%);
            }
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .main-title {
                font-size: 2.5rem;
                letter-spacing: 8px;
                height: 60px;
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
            
            .bottom-navigation {
                height: 70px;
            }
            
            .nav-icon {
                font-size: 1.5rem;
            }
            
            .nav-label {
                font-size: 0.8rem;
            }
            
            .footer-button-container {
                flex-direction: row;
                flex-wrap: wrap;
                gap: 10px;
                bottom: 70px;
            }
            
            .back-button, .switch-button {
                min-width: 120px;
                width: calc(33.333% - 10px);
                max-width: 160px;
                padding: 8px 12px;
                font-size: 0.85rem;
            }
            
            .company-placeholder-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }
            
            .company-placeholder-item {
                padding: 20px 10px;
                font-size: 1.3rem;
                min-height: 100px;
            }
        }
        
        @media (max-width: 480px) {
            .main-title {
                font-size: 2rem;
                letter-spacing: 5px;
                height: 50px;
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
            
            .bottom-navigation {
                height: 65px;
            }
            
            .nav-icon {
                font-size: 1.3rem;
                margin-bottom: 3px;
            }
            
            .nav-label {
                font-size: 0.7rem;
            }
            
            .footer-button-container {
                flex-direction: row;
                flex-wrap: wrap;
                gap: 8px;
                bottom: 65px;
            }
            
            .back-button, .switch-button {
                min-width: 100px;
                width: calc(50% - 8px);
                max-width: 140px;
                padding: 6px 10px;
                font-size: 0.8rem;
            }
            
            .company-placeholder-grid {
                grid-template-columns: 1fr;
                gap: 10px;
            }
            
            .company-placeholder-item {
                padding: 15px 10px;
                font-size: 1.2rem;
                min-height: 80px;
            }
        }
        
        @media (max-width: 360px) {
            .footer-button-container {
                flex-direction: column;
                align-items: center;
                bottom: 65px;
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
    <!-- 视觉层 -->
    <div class="ambient-light"></div>
    <div class="scan-line"></div>
    
    <!-- 状态指示器 -->
    <div class="status-indicator neon-glow" id="statusIndicator">CH-AI 系统: 初始化</div>
    
    <!-- 底部导航栏 -->
    <div class="bottom-navigation hidden" id="bottomNavigation">
        <div class="nav-slide-area" id="navSlideArea"></div>
        <div class="nav-slider" id="navSlider"></div>
        
        <div class="nav-item active" data-target="timescreen">
            <i class="fas fa-newspaper nav-icon"></i>
            <span class="nav-label">时报</span>
        </div>
        
        <div class="nav-item" data-target="database">
            <i class="fas fa-database nav-icon"></i>
            <span class="nav-label">数据库</span>
        </div>
        
        <div class="nav-item" data-target="map">
            <i class="fas fa-map nav-icon"></i>
            <span class="nav-label">地图</span>
        </div>
    </div><!-- 加载界面 -->
<div class="loading-screen" id="loadingScreen">
    <div class="title-container">
        <h1 class="main-title neon-glow" id="mainTitle">
            <span id="titleLetters"></span>
        </h1>
        <div class="subtitle">采用CH级城市管理AI技术 • 访问模式</div>
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
        <span class="final-message-text neon-glow">一切为了██</span>
    </div>
    
    <!-- 进入系统按钮 -->
    <button class="menu-button neon-glow" id="menuButton">
        <span class="button-text">进入系统</span>
        <span class="button-glow"></span>
    </button>
</div>

<!-- 时报界面 - 第一个界面 -->
<div class="menu-screen" id="timescreen">
    <div class="menu-header">
        <h2 class="menu-title neon-glow">梦羊城时报</h2>
        <div class="menu-subtitle">CH-AI 实时新闻系统 v2.4.1 • 终端</div>
    </div>
    
    <div class="menu-content">
        <!-- 今日头条 -->
        <div class="menu-section">
            <div class="section-header" data-target="headline-news">
                <i class="fas fa-newspaper" style="margin-right: 10px;"></i>
                今日头条
            </div>
            <div class="section-content" id="headline-news">
                <div class="timescreen-article">
                    <div class="article-title">
                        <span class="article-date">2025-11-23</span>
                        <span>我自行输入文本</span>
                    </div>
                    <div class="article-content">
                        <p>我自行输入文本</p>
                        <p>我自行输入文本</p>
                    </div>
                    <div>
                        <span class="article-tag"><i class="fas fa-microchip"></i> 科技</span>
                        <span class="article-tag"><i class="fas fa-robot"></i> CH-AI</span>
                        <span class="article-tag"><i class="fas fa-sync-alt"></i> 系统升级</span>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 城市动态 -->
        <div class="menu-section">
            <div class="section-header" data-target="city-dynamics">
                <i class="fas fa-city" style="margin-right: 10px;"></i>
                城市动态
            </div>
            <div class="section-content" id="city-dynamics">
                <div class="timescreen-article">
                    <div class="article-title">
                        <span class="article-date">2025-1-22</span>
                        <span>我自行输入文本</span>
                    </div>
                    <div class="article-content">
                        <p>我自行输入文本</p>
                        <p>我自行输入文本</p>
                    </div>
                    <div>
                        <span class="article-tag"><i class="fas fa-leaf"></i> 农业</span>
                        <span class="article-tag"><i class="fas fa-building"></i> 城市建设</span>
                        <span class="article-tag"><i class="fas fa-recycle"></i> 可持续发展</span>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 科技前沿 -->
        <div class="menu-section">
            <div class="section-header" data-target="tech-frontier">
                <i class="fas fa-flask" style="margin-right: 10px;"></i>
                科技前沿
            </div>
            <div class="section-content" id="tech-frontier">
                <div class="timescreen-article">
                    <div class="article-title">
                        <span class="article-date">2025-1-20</span>
                        <span>我自行输入文本</span>
                    </div>
                    <div class="article-content">
                        <p>我自行输入文本</p>
                        <p>我自行输入文本</p>
                    </div>
                    <div>
                        <span class="article-tag"><i class="fas fa-atom"></i> 科研</span>
                        <span class="article-tag"><i class="fas fa-globe-americas"></i> 跨维度</span>
                        <span class="article-tag"><i class="fas fa-satellite"></i> 通信技术</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 时报底部按钮 -->
    <div class="footer-button-container">
        <button class="back-button" id="timescreenBackButton">
            <i class="fas fa-home" style="margin-right: 8px;"></i>返回加载界面
        </button>
    </div>
</div>

<!-- 数据库界面 - 第二个界面 -->
<div class="database-screen" id="databaseScreen">
    <div class="menu-header">
        <h2 class="menu-title neon-glow">梦羊城数据库</h2>
        <div class="menu-subtitle">CH-AI 中央档案系统 v3.7.2 • 访问权限</div>
    </div>    <div class="menu-content">
        <!-- 1. 编年史 -->
        <div class="menu-section">
            <div class="section-header" data-target="chronicles">
                <i class="fas fa-scroll" style="margin-right: 10px;"></i>
                编年史
            </div>
            <div class="section-content" id="chronicles">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 2. 公司 -->
        <div class="menu-section">
            <div class="section-header" data-target="company">
                <i class="fas fa-industry" style="margin-right: 10px;"></i>
                公司
            </div>
            <div class="section-content" id="company">
                <div class="content-text">
                    我自行输入文本
                    <br><br>
                    <button class="switch-button" id="openCompanyHistoryButton" style="margin-top: 15px;">
                        <i class="fas fa-history" style="margin-right: 8px;"></i>查看公司历史档案
                    </button>
                </div>
            </div>
        </div>
        
        <!-- 3. 种族 -->
        <div class="menu-section">
            <div class="section-header" data-target="races">
                <i class="fas fa-users" style="margin-right: 10px;"></i>
                种族
            </div>
            <div class="section-content" id="races">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 4. 民间组织 -->
        <div class="menu-section">
            <div class="section-header" data-target="civilian-orgs">
                <i class="fas fa-hands-helping" style="margin-right: 10px;"></i>
                民间组织
            </div>
            <div class="section-content" id="civilian-orgs">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 5. 神秘术 -->
        <div class="menu-section">
            <div class="section-header" data-target="mysticism">
                <i class="fas fa-magic" style="margin-right: 10px;"></i>
                神秘术
            </div>
            <div class="section-content" id="mysticism">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 6. 官方组织 -->
        <div class="menu-section">
            <div class="section-header" data-target="official-orgs">
                <i class="fas fa-landmark" style="margin-right: 10px;"></i>
                官方组织
            </div>
            <div class="section-content" id="official-orgs">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 7. 梅林坐标系 -->
        <div class="menu-section">
            <div class="section-header" data-target="merlin-coordinates">
                <i class="fas fa-crosshairs" style="margin-right: 10px;"></i>
                梅林坐标系
            </div>
            <div class="section-content" id="merlin-coordinates">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
        
        <!-- 8. 政权 -->
        <div class="menu-section">
            <div class="section-header" data-target="government">
                <i class="fas fa-crown" style="margin-right: 10px;"></i>
                政权
            </div>
            <div class="section-content" id="government">
                <div class="content-text">
                    我自行输入文本
                </div>
            </div>
        </div>
    </div>
    
    <!-- 数据库底部按钮 -->
    <div class="footer-button-container">
        <button class="back-button" id="databaseBackButton">
            <i class="fas fa-home" style="margin-right: 8px;"></i>返回加载界面
        </button>
    </div>
</div>

<!-- 地图界面 - 第三个界面 -->
<div class="map-screen" id="mapScreen">
    <div class="menu-header">
        <h2 class="menu-title neon-glow">梦羊城地图</h2>
        <div class="menu-subtitle">CH-AI 空间导航系统 v1.5.3 • 坐标系激活</div>
    </div>
    
    <div class="menu-content">
        <div class="map-placeholder">
            <i class="fas fa-map-marked-alt" style="font-size: 3rem; margin-bottom: 20px; display: block;"></i>
            地图系统正在开发中...
            <br>
            <br>
            坐标系加载中...
            <br>
            <br>
            <div style="color: #00ff00; margin: 10px 0;">
                <i class="fas fa-circle" style="color: #00ff00;"></i> 当前维度：正常
            </div>
            <div style="color: #00ff00; margin: 10px 0;">
                <i class="fas fa-check-circle" style="color: #00ff00;"></i> 状态：稳定
            </div>
            <div style="color: #ffaa66; margin-top: 20px; font-size: 1rem;">
                <i class="fas fa-info-circle"></i> 空间导航功能即将上线
            </div>
        </div>
    </div>
    
    <!-- 地图底部按钮 -->
    <div class="footer-button-container">
        <button class="back-button" id="mapBackButton">
            <i class="fas fa-home" style="margin-right: 8px;"></i>返回加载界面
        </button>
    </div>
</div><!-- 公司历史界面 - 第四个界面 -->
<div class="company-history-screen" id="companyHistoryScreen">
    <div class="menu-header">
        <h2 class="menu-title neon-glow">梦羊城公司历史档案</h2>
        <div class="menu-subtitle">公司档案索引 • 访问权限</div>
    </div>
    
    <div class="menu-content">
        <div class="company-placeholder-grid" id="companyPlaceholderGrid">
            <!-- 6个占位符将通过JavaScript动态生成 -->
        </div>
    </div>
    
    <!-- 公司历史界面底部按钮 -->
    <div class="footer-button-container">
        <button class="back-button" id="companyHistoryBackButton">
            <i class="fas fa-arrow-left" style="margin-right: 8px;"></i>返回数据库
        </button>
    </div>
</div>

<!-- 公司详情界面 - 第五个界面（静态展示） -->
<div class="company-detail-screen" id="companyDetailScreen">
    <div class="menu-header">
        <h2 class="menu-title neon-glow" id="companyDetailTitle">公司档案详情</h2>
        <div class="menu-subtitle">公司档案详情 • 安全访问</div>
    </div>
    
    <div class="menu-content">
        <!-- 静态详情内容区域 -->
        <div class="static-detail-content" id="staticDetailContent">
            <!-- 静态内容将通过JavaScript动态生成 -->
        </div>
    </div>
    
    <!-- 公司详情界面底部按钮 -->
    <div class="footer-button-container">
        <button class="back-button" id="companyDetailBackButton">
            <i class="fas fa-arrow-left" style="margin-right: 8px;"></i>返回公司历史
        </button>
    </div>
</div>

<script>
    // 等待DOM完全加载
    document.addEventListener('DOMContentLoaded', function() {
        console.log("DOM加载完成，开始系统初始化...");
        
        // 获取主界面元素
        const loadingScreen = document.getElementById('loadingScreen');
        const timescreen = document.getElementById('timescreen');
        const databaseScreen = document.getElementById('databaseScreen');
        const mapScreen = document.getElementById('mapScreen');
        const companyHistoryScreen = document.getElementById('companyHistoryScreen');
        const companyDetailScreen = document.getElementById('companyDetailScreen');
        const loadingBar = document.getElementById('loadingBar');
        const percentage = document.getElementById('percentage');
        const loadingText = document.getElementById('loadingText');
        const finalMessage = document.getElementById('finalMessage');
        const menuButton = document.getElementById('menuButton');
        const statusIndicator = document.getElementById('statusIndicator');
        const titleLettersContainer = document.getElementById('titleLetters');
        
        // 获取底部导航栏元素
        const bottomNavigation = document.getElementById('bottomNavigation');
        const navSlideArea = document.getElementById('navSlideArea');
        const navSlider = document.getElementById('navSlider');
        const navItems = document.querySelectorAll('.nav-item');
        
        // 获取主界面按钮元素
        const timescreenBackButton = document.getElementById('timescreenBackButton');
        const databaseBackButton = document.getElementById('databaseBackButton');
        const mapBackButton = document.getElementById('mapBackButton');
        
        // 获取公司历史界面按钮元素
        const openCompanyHistoryButton = document.getElementById('openCompanyHistoryButton');
        const companyHistoryBackButton = document.getElementById('companyHistoryBackButton');
        
        // 获取公司详情界面按钮元素
        const companyDetailBackButton = document.getElementById('companyDetailBackButton');
        
        // 获取内容容器元素
        const companyPlaceholderGrid = document.getElementById('companyPlaceholderGrid');
        const staticDetailContent = document.getElementById('staticDetailContent');
        const companyDetailTitle = document.getElementById('companyDetailTitle');
        
        // 检查元素是否找到
        const essentialElements = [loadingScreen, timescreen, databaseScreen, mapScreen, loadingBar, 
                                  percentage, loadingText, finalMessage, menuButton, statusIndicator, 
                                  bottomNavigation];
        
        for (const element of essentialElements) {
            if (!element) {
                console.error("部分元素未找到，请检查HTML结构");
                return;
            }
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
        companyHistoryScreen.style.display = 'none';
        companyDetailScreen.style.display = 'none';
        bottomNavigation.classList.add('hidden');
        
        // 初始化英文标题字母
        const titleText = "DREAM GOAT CITY";
        let titleLetters = [];
        
        // 创建音频上下文（用于生成音效）
        let audioContext;
        let isAudioContextInitialized = false;
        let lastSoundTime = 0; // 记录上次播放音效的时间
        const SOUND_COOLDOWN = 100; // 音效冷却时间(毫秒)，避免连续播放
        
        // 高级视觉光标
        let advancedCursor = null;
        
        // 当前激活的屏幕
        let activeScreen = 'loading';
        
        // 加载消息
        const loadingMessages = [
            "初始化神经接口...",
            "校准梅林坐标系...",
            "加载城市AI核心...",
            "验证访问权限...",
            "同步时间线数据...",
            "建立安全连接...",
            "准备用户界面..."
        ];
        
        // 记录小标题点击时间和次数
        const clickHistory = {};
        const ERROR_COOLDOWN = 300; // 错误效果冷却时间(ms)
        const RAPID_CLICK_THRESHOLD = 3; // 快速点击次数阈值
        const RAPID_CLICK_WINDOW = 1000; // 快速点击时间窗口(ms)
        
        // 加载阶段
        const loadingStages = [
            { text: "正在进行精神检测", percent: 30 },
            { text: "正在进行面部解析", percent: 60 },
            { text: "正在加固防火墙", percent: 80 },
            { text: "预加载界面", percent: 95 },
            { text: "完成安全协议", percent: 100 }
        ];
        
        let currentStage = 0;
        let currentPercent = 0;
        let isLoaded = false;
        let lastProgressUpdate = 0;
        const PROGRESS_UPDATE_INTERVAL = 20; // 加快更新频率到20ms
        
        // 界面列表（用于滑动切换）
        const screens = [
            { id: 'timescreen', name: '时报' },
            { id: 'database', name: '数据库' },
            { id: 'map', name: '地图' }
        ];
        
        let currentScreenIndex = 0;
        
        // 滑动相关变量
        let isDragging = false;
        let startX = 0;
        let startY = 0;
        let dragThreshold = 30; // 滑动阈值
        
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
        }// 键盘按键音效
function playKeyboardSound(type = 'click') {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        // 根据类型调整音效
        if (type === 'click') {
            // 键盘点击声
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
            // 空格键音效
            oscillator.type = 'sine';
            oscillator.frequency.setValueAtTime(200, audioContext.currentTime);
            oscillator.frequency.exponentialRampToValueAtTime(100, audioContext.currentTime + 0.12);
            
            gainNode.gain.setValueAtTime(0.07, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
            
            oscillator.start();
            oscillator.stop(audioContext.currentTime + 0.15);
        } else if (type === 'hover') {
            // 悬停音效
            oscillator.type = 'sine';
            oscillator.frequency.setValueAtTime(1000, audioContext.currentTime);
            oscillator.frequency.exponentialRampToValueAtTime(1200, audioContext.currentTime + 0.05);
            
            gainNode.gain.setValueAtTime(0.03, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.1);
            
            oscillator.start();
            oscillator.stop(audioContext.currentTime + 0.1);
        }
        
        console.log(`播放键盘音效: ${type}`);
    } catch (error) {
        console.error("播放键盘音效时出错:", error);
    }
}

// 故障音效
function playGlitchSound() {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const oscillator1 = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator1.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        // 数字故障音效
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

// 加载界面故障音效
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

// 扫描线音效
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

// 数据库操作音效
function playDatabaseSound() {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        // 数据库操作的确认音
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
}// 地图音效
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

// 过渡音效
function playTransitionSound() {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const context = audioContext;
        const now = context.currentTime;
        
        // 创建主音调
        const oscillator1 = context.createOscillator();
        const gain1 = context.createGain();
        oscillator1.connect(gain1);
        gain1.connect(context.destination);
        
        oscillator1.type = 'sine';
        oscillator1.frequency.setValueAtTime(200, now);
        oscillator1.frequency.exponentialRampToValueAtTime(600, now + 0.3);
        oscillator1.frequency.exponentialRampToValueAtTime(400, now + 0.6);
        
        gain1.gain.setValueAtTime(0, now);
        gain1.gain.linearRampToValueAtTime(0.1, now + 0.1);
        gain1.gain.exponentialRampToValueAtTime(0.001, now + 0.7);
        
        // 创建氛围音
        const oscillator2 = context.createOscillator();
        const gain2 = context.createGain();
        oscillator2.connect(gain2);
        gain2.connect(context.destination);
        
        oscillator2.type = 'triangle';
        oscillator2.frequency.setValueAtTime(100, now);
        oscillator2.frequency.linearRampToValueAtTime(150, now + 0.6);
        
        gain2.gain.setValueAtTime(0, now);
        gain2.gain.linearRampToValueAtTime(0.03, now + 0.2);
        gain2.gain.exponentialRampToValueAtTime(0.001, now + 0.7);
        
        oscillator1.start(now);
        oscillator2.start(now);
        oscillator1.stop(now + 0.7);
        oscillator2.stop(now + 0.7);
        
        console.log("播放过渡音效");
    } catch (error) {
        console.error("播放过渡音效时出错:", error);
    }
}

// 字母悬停音效
function playLetterHoverSound() {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        oscillator.type = 'sine';
        oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
        oscillator.frequency.exponentialRampToValueAtTime(1000, audioContext.currentTime + 0.1);
        
        gainNode.gain.setValueAtTime(0.02, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
        
        oscillator.start();
        oscillator.stop(audioContext.currentTime + 0.15);
    } catch (error) {
        console.error("播放字母悬停音效时出错:", error);
    }
}

// 导航切换音效
function playNavSwitchSound() {
    if (!isAudioContextInitialized || !canPlaySound()) return;
    
    try {
        const oscillator1 = audioContext.createOscillator();
        const oscillator2 = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator1.connect(gainNode);
        oscillator2.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        // 双音调切换音效
        oscillator1.type = 'sine';
        oscillator2.type = 'sine';
        
        oscillator1.frequency.setValueAtTime(400, audioContext.currentTime);
        oscillator2.frequency.setValueAtTime(600, audioContext.currentTime);
        
        oscillator1.frequency.exponentialRampToValueAtTime(500, audioContext.currentTime + 0.1);
        oscillator2.frequency.exponentialRampToValueAtTime(700, audioContext.currentTime + 0.1);
        
        gainNode.gain.setValueAtTime(0.04, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.001, audioContext.currentTime + 0.15);
        
        oscillator1.start();
        oscillator2.start();
        oscillator1.stop(audioContext.currentTime + 0.15);
        oscillator2.stop(audioContext.currentTime + 0.15);
    } catch (error) {
        console.error("播放导航切换音效时出错:", error);
    }
}

// 更新状态指示器
function updateStatus(text) {
    if (statusIndicator) {
        statusIndicator.textContent = `CH-AI 系统: ${text}`;
    }
}

// 故障效果
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
}// 触发频繁点击报错效果
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

// 创建英文标题字母元素
function createTitleLetters() {
    if (!titleLettersContainer) return;
    
    titleLettersContainer.innerHTML = '';
    titleLetters = [];
    
    // 创建字母元素
    for (let i = 0; i < titleText.length; i++) {
        const char = titleText.charAt(i);
        const span = document.createElement('span');
        span.className = 'title-letter';
        span.textContent = char === ' ' ? '\u00A0' : char;
        span.style.transitionDelay = `${i * 0.05}s`;
        
        titleLettersContainer.appendChild(span);
        titleLetters.push(span);
    }
    
    console.log("创建英文标题字母元素");
}

// 显示标题字母
function showTitleLetters(percent) {
    if (!titleLetters || titleLetters.length === 0) return;
    
    // 根据进度计算要显示的字母数量
    const lettersToShow = Math.floor((percent / 100) * titleLetters.length);
    
    // 显示对应数量的字母
    for (let i = 0; i < titleLetters.length; i++) {
        if (i < lettersToShow) {
            titleLetters[i].classList.add('visible');
        } else {
            titleLetters[i].classList.remove('visible');
        }
    }
}

// 增强标题字母动画
function enhanceTitleAnimation() {
    if (!titleLetters || titleLetters.length === 0) return;
    
    titleLetters.forEach((letter, index) => {
        // 为每个字母添加独立动画延迟
        letter.style.transitionDelay = `${index * 0.05}s`;
        
        // 添加入场动画
        letter.style.opacity = '0';
        letter.style.transform = 'translateY(20px) rotateX(90deg)';
        
        // 添加悬停效果
        letter.addEventListener('mouseenter', () => {
            if (isLoaded) {
                letter.style.transform = 'translateY(-5px) scale(1.2)';
                letter.style.color = '#ff8844';
                letter.style.textShadow = '0 0 10px rgba(255, 136, 68, 0.8)';
                
                // 播放悬停音效
                if (isAudioContextInitialized && canPlaySound()) {
                    playLetterHoverSound();
                }
            }
        });
        
        letter.addEventListener('mouseleave', () => {
            if (isLoaded) {
                letter.style.transform = 'translateY(0) scale(1)';
                letter.style.color = '#ff6600';
                letter.style.textShadow = '';
            }
        });
    });  
}

// 页面过渡效果
function createPageTransition(fromScreen, toScreen, callback) {
    // 创建过渡遮罩
    const transitionOverlay = document.createElement('div');
    transitionOverlay.className = 'page-transition';
    document.body.appendChild(transitionOverlay);
    
    // 播放过渡音效
    playTransitionSound();
    
    // 执行过渡
    setTimeout(() => {
        if (fromScreen) fromScreen.style.display = 'none';
        if (toScreen) {
            toScreen.style.display = 'flex';
            toScreen.classList.add('fade-in');
        }
        
        // 移除过渡元素
        setTimeout(() => {
            transitionOverlay.remove();
            if (callback) callback();
        }, 600);
    }, 300);
}

// 加载消息模拟
function simulateLoading() {
    let messageIndex = 0;
    const messageInterval = setInterval(() => {
        if (messageIndex < loadingMessages.length && loadingText) {
            const message = loadingMessages[messageIndex];
            
            // 添加打字机效果
            const originalText = message;
            loadingText.textContent = '';
            let charIndex = 0;
            
            const typeWriter = setInterval(() => {
                if (charIndex < originalText.length) {
                    loadingText.textContent += originalText.charAt(charIndex);
                    charIndex++;
                } else {
                    clearInterval(typeWriter);
                }
            }, 50);
            
            messageIndex++;
            
        } else {
            clearInterval(messageInterval);
        }
    }, 800);
}

// 鼠标跟随效果
function initMouseFollow() {
    const cursor = document.createElement('div');
    cursor.className = 'advanced-cursor';
    document.body.appendChild(cursor);
    advancedCursor = cursor;
    
    // 鼠标移动事件
    document.addEventListener('mousemove', (e) => {
        if (advancedCursor) {
            advancedCursor.style.left = e.clientX + 'px';
            advancedCursor.style.top = e.clientY + 'px';
        }
    });
    
    // 悬停效果
    const interactiveElements = document.querySelectorAll('button, .section-header, .company-placeholder-item, .title-letter, .nav-item');
    interactiveElements.forEach(el => {
        el.addEventListener('mouseenter', () => {
            if (advancedCursor) {
                advancedCursor.classList.add('hover');
            }
            playKeyboardSound('hover');
        });
        
        el.addEventListener('mouseleave', () => {
            if (advancedCursor) {
                advancedCursor.classList.remove('hover');
            }
        });
    });
    
    // 点击效果
    document.addEventListener('mousedown', () => {
        if (advancedCursor) {
            advancedCursor.classList.add('click');
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (advancedCursor) {
            advancedCursor.classList.remove('click');
        }
    });
}// 视差滚动效果
function initParallaxEffect() {
    const scanLine = document.querySelector('.scan-line');
    const ambientLight = document.querySelector('.ambient-light');
    
    window.addEventListener('scroll', () => {
        const scrolled = window.pageYOffset;
        const rate = scrolled * -0.5;
        
        if (scanLine) {
            scanLine.style.transform = `translateY(${rate}px)`;
        }
        
        if (ambientLight) {
            ambientLight.style.transform = `translateY(${rate * 0.2}px)`;
        }
    });
}

// 内容显示动画
function enhanceContentReveal() {
    const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
    };
    
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('fade-in');
                observer.unobserve(entry.target);
            }
        });
    }, observerOptions);
    
    // 观察所有内容元素
    const contentElements = document.querySelectorAll('.timescreen-article, .content-text, .company-placeholder-item, .static-detail-content');
    contentElements.forEach(el => {
        observer.observe(el);
    });
}

// 更新进度条
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
            
            // 更新标题字母显示
            showTitleLetters(currentPercent);
            
            // 加载界面错误特效 - 更频繁的触发
            if (Math.random() < 0.15 && loadingText) {
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
                }, 200);
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
        loadingText.textContent = "系统就绪 • 终端激活";
    }
    updateStatus("模式就绪");
    
    // 确保所有标题字母都显示
    showTitleLetters(100);
    
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
        updateStatus("一切为了██ • 访问授权");
        
        // 增强噪点效果
        const noiseOverlay = finalMessage.querySelector('.noise-overlay');
        if (noiseOverlay) {
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
                
                // 绑定进入系统按钮事件
                menuButton.addEventListener('click', openTimescreen);
                console.log("菜单按钮事件已绑定");
            }
        }, 300);
    }, 300);
}

// ========== 底部导航栏功能 ==========

// 切换导航栏活动状态
function updateNavActiveState(targetScreen) {
    // 移除所有活动的导航项
    navItems.forEach(item => {
        item.classList.remove('active');
    });
    
    // 激活对应的导航项
    const targetNavItem = document.querySelector(`.nav-item[data-target="${targetScreen}"]`);
    if (targetNavItem) {
        targetNavItem.classList.add('active');
    }
    
    // 更新当前屏幕索引
    currentScreenIndex = screens.findIndex(screen => screen.id === targetScreen);
}

// 显示底部导航栏
function showBottomNavigation() {
    bottomNavigation.classList.remove('hidden');
}

// 隐藏底部导航栏
function hideBottomNavigation() {
    bottomNavigation.classList.add('hidden');
}

// 切换到指定界面
function switchToScreen(screenId, playSound = true) {
    console.log(`切换到界面: ${screenId}`);
    
    if (playSound) {
        playNavSwitchSound();
    }
    
    // 隐藏所有界面
    const allScreens = [timescreen, databaseScreen, mapScreen, companyHistoryScreen, companyDetailScreen];
    allScreens.forEach(screen => {
        if (screen) screen.style.display = 'none';
    });
    
    // 显示目标界面
    let targetScreen;
    switch(screenId) {
        case 'timescreen':
            targetScreen = timescreen;
            updateStatus("访问时报 • 终端");
            break;
        case 'database':
            targetScreen = databaseScreen;
            updateStatus("访问数据库 • 权限");
            break;
        case 'map':
            targetScreen = mapScreen;
            updateStatus("访问地图 • 梅林坐标系");
            break;
        default:
            targetScreen = timescreen;
    }
    
    if (targetScreen) {
        targetScreen.style.display = 'flex';
        targetScreen.classList.add('fade-in');
        
        // 滚动到顶部
        setTimeout(() => {
            targetScreen.scrollTop = 0;
        }, 100);
    }
    
    // 更新导航栏状态
    updateNavActiveState(screenId);
    activeScreen = screenId;
    
    // 显示底部导航栏（如果是主界面）
    if (screenId === 'timescreen' || screenId === 'database' || screenId === 'map') {
        showBottomNavigation();
    } else {
        hideBottomNavigation();
    }
    }// 初始化底部导航栏滑动功能
function initBottomNavSwipe() {
    if (!navSlideArea) return;
    
    // 触摸事件
    navSlideArea.addEventListener('touchstart', handleTouchStart, { passive: false });
    navSlideArea.addEventListener('touchmove', handleTouchMove, { passive: false });
    navSlideArea.addEventListener('touchend', handleTouchEnd);
    
    // 鼠标事件
    navSlideArea.addEventListener('mousedown', handleMouseDown);
    navSlideArea.addEventListener('mousemove', handleMouseMove);
    navSlideArea.addEventListener('mouseup', handleMouseUp);
    navSlideArea.addEventListener('mouseleave', handleMouseUp);
    
    // 激活滑动指示器
    navSlider.classList.add('active');
}

// 触摸事件处理
function handleTouchStart(e) {
    e.preventDefault();
    isDragging = true;
    startX = e.touches[0].clientX;
    startY = e.touches[0].clientY;
}

function handleTouchMove(e) {
    if (!isDragging) return;
    e.preventDefault();
    
    const currentX = e.touches[0].clientX;
    const currentY = e.touches[0].clientY;
    
    // 检查是否为水平滑动
    const deltaX = Math.abs(currentX - startX);
    const deltaY = Math.abs(currentY - startY);
    
    // 如果垂直滑动超过阈值，取消滑动
    if (deltaY > dragThreshold && deltaY > deltaX) {
        isDragging = false;
        return;
    }
    
    // 处理水平滑动
    if (deltaX > dragThreshold) {
        const direction = currentX > startX ? 'right' : 'left';
        handleSwipe(direction);
        isDragging = false;
    }
}

function handleTouchEnd() {
    isDragging = false;
}

// 鼠标事件处理
function handleMouseDown(e) {
    e.preventDefault();
    isDragging = true;
    startX = e.clientX;
    startY = e.clientY;
}

function handleMouseMove(e) {
    if (!isDragging) return;
    e.preventDefault();
    
    const currentX = e.clientX;
    const currentY = e.clientY;
    
    // 检查是否为水平滑动
    const deltaX = Math.abs(currentX - startX);
    const deltaY = Math.abs(currentY - startY);
    
    // 如果垂直滑动超过阈值，取消滑动
    if (deltaY > dragThreshold && deltaY > deltaX) {
        isDragging = false;
        return;
    }
    
    // 处理水平滑动
    if (deltaX > dragThreshold) {
        const direction = currentX > startX ? 'right' : 'left';
        handleSwipe(direction);
        isDragging = false;
    }
}

function handleMouseUp() {
    isDragging = false;
}

// 处理滑动方向
function handleSwipe(direction) {
    console.log(`滑动方向: ${direction}`);
    
    // 播放滑动音效
    playKeyboardSound('space');
    
    let newIndex = currentScreenIndex;
    
    if (direction === 'left') {
        // 向左滑动，切换到下一个界面
        newIndex = (currentScreenIndex + 1) % screens.length;
    } else if (direction === 'right') {
        // 向右滑动，切换到上一个界面
        newIndex = (currentScreenIndex - 1 + screens.length) % screens.length;
    }
    
    // 切换到新界面
    if (newIndex !== currentScreenIndex) {
        const targetScreen = screens[newIndex].id;
        switchToScreen(targetScreen);
    }
}

// 打开时报（第一个界面）
function openTimescreen() {
    console.log("打开时报界面");
    playKeyboardSound('enter');
    
    const title = document.querySelector('.main-title');
    triggerGlitch(title);
    
    // 隐藏加载界面
    loadingScreen.style.display = 'none';
    
    // 切换到时报界面
    switchToScreen('timescreen', false);
}

// 打开公司历史界面（第四个界面）
function openCompanyHistory() {
    console.log("打开公司历史界面");
    playDatabaseSound();
    
    const menuTitle = document.querySelector('.menu-title');
    triggerGlitch(menuTitle);
    updateStatus("访问公司历史档案 • 检索");
    
    // 生成公司历史占位符
    generateCompanyHistoryPlaceholders();
    
    // 隐藏数据库界面
    databaseScreen.style.display = 'none';
    
    // 显示公司历史界面
    companyHistoryScreen.style.display = 'flex';
    companyHistoryScreen.classList.add('fade-in');
    
    // 隐藏底部导航栏
    hideBottomNavigation();
    
    activeScreen = 'company-history';
    
    // 滚动到顶部
    setTimeout(() => {
        companyHistoryScreen.scrollTop = 0;
    }, 100);
}

// 打开公司详情界面（第五个界面）
function openCompanyDetail(companyIndex) {
    console.log(`打开公司详情界面，公司索引: ${companyIndex}`);
    playKeyboardSound('click');
    
    updateStatus(`访问公司档案 #${companyIndex} • 查看`);
    
    // 设置标题
    if (companyDetailTitle) {
        companyDetailTitle.textContent = `公司档案 #${companyIndex}`;
    }
    
    // 生成静态详情内容
    generateStaticDetailContent(companyIndex);
    
    // 隐藏公司历史界面
    companyHistoryScreen.style.display = 'none';
    
    // 显示公司详情界面
    companyDetailScreen.style.display = 'flex';
    companyDetailScreen.classList.add('fade-in');
    
    activeScreen = 'company-detail';
    
    // 滚动到顶部
    setTimeout(() => {
        companyDetailScreen.scrollTop = 0;
    }, 100);
}

// 关闭菜单返回加载界面
function closeToLoading() {
    console.log("返回加载界面");
    playKeyboardSound('space');
    
    const currentTitle = document.querySelector('.menu-title');
    triggerGlitch(currentTitle);
    updateStatus("返回加载界面 • 系统待机");
    
    // 隐藏当前界面
    const allScreens = [timescreen, databaseScreen, mapScreen, companyHistoryScreen, companyDetailScreen];
    allScreens.forEach(screen => {
        if (screen) screen.style.display = 'none';
    });
    
    // 显示加载界面
    loadingScreen.style.display = 'flex';
    
    // 隐藏底部导航栏
    hideBottomNavigation();
    
    activeScreen = 'loading';
}

// 返回数据库界面
function backToDatabase() {
    console.log("返回数据库界面");
    playKeyboardSound('space');
    
    const menuTitle = document.querySelector('.menu-title');
    triggerGlitch(menuTitle);
    updateStatus("返回数据库 • 继续访问");
    
    // 隐藏公司历史界面
    companyHistoryScreen.style.display = 'none';
    
    // 切换到数据库界面
    switchToScreen('database', false);
}

// 返回公司历史界面
function backToCompanyHistory() {
    console.log("返回公司历史界面");
    playKeyboardSound('space');
    
    const menuTitle = document.querySelector('.menu-title');
    triggerGlitch(menuTitle);
    updateStatus("返回公司历史档案 • 继续检索");
    
    // 隐藏公司详情界面
    companyDetailScreen.style.display = 'none';
    
    // 显示公司历史界面
    companyHistoryScreen.style.display = 'flex';
    companyHistoryScreen.classList.add('fade-in');
    
    activeScreen = 'company-history';
    
    // 滚动到顶部
    setTimeout(() => {
        companyHistoryScreen.scrollTop = 0;
    }, 100);
}

// 切换菜单项
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
        updateStatus(`访问: ${menuText} • 查看`);
        
        // 添加故障效果
        triggerGlitch(header);
    }
          }
          // 生成公司历史占位符（6个）
function generateCompanyHistoryPlaceholders() {
    if (!companyPlaceholderGrid) return;
    
    companyPlaceholderGrid.innerHTML = '';
    
    const companyNames = [
        "都市动力学公司",
        "梅林科技集团", 
        "维度通信公司",
        "神经接口科技",
        "垂直农场联合体",
        "时间线研究机构"
    ];
    
    for (let i = 1; i <= 6; i++) {
        const placeholderItem = document.createElement('div');
        placeholderItem.className = 'company-placeholder-item';
        placeholderItem.innerHTML = `
            <div style="text-align: center;">
                <div style="font-size: 2rem; margin-bottom: 10px;">${i}</div>
                <div style="font-size: 0.9rem; color: #ffaa66;">${companyNames[i-1]}</div>
            </div>
        `;
        placeholderItem.dataset.companyIndex = i;
        
        // 添加点击事件
        placeholderItem.addEventListener('click', function() {
            const companyIndex = parseInt(this.dataset.companyIndex);
            openCompanyDetail(companyIndex);
        });
        
        // 添加悬停音效
        placeholderItem.addEventListener('mouseenter', () => {
            playKeyboardSound('hover');
        });
        
        companyPlaceholderGrid.appendChild(placeholderItem);
    }
    
    console.log("生成6个公司历史占位符");
}

// 生成静态详情内容
function generateStaticDetailContent(companyIndex) {
    if (!staticDetailContent) return;
    
    const companyNames = [
        "都市动力学公司",
        "梅林科技集团", 
        "维度通信公司",
        "神经接口科技",
        "垂直农场联合体",
        "时间线研究机构"
    ];
    
    const companyDescriptions = [
        "负责梦羊城基础设施维护与管理的核心技术公司，掌握城市动力系统的最高权限。",
        "专注于跨维度科技研究的先锋企业，梅林坐标系的发明者和维护者。",
        "实现平行宇宙间稳定通信的科技巨头，推动梦羊城成为跨维度交流中心。",
        "人机接口技术的领导者，为市民提供无缝的神经连接体验。",
        "城市食品供应的保障者，采用最先进的垂直农业技术实现粮食自给自足。",
        "时间线研究与维护的权威机构，确保梦羊城时间流的稳定性与安全性。"
    ];
    
    const founders = [
        "亚历山大·陈博士",
        "梅林·奥古斯都",
        "赛琳娜·维度",
        "诺亚·神经桥",
        "绿谷耕作",
        "克罗诺斯·时刻"
    ];
    
    // 静态内容模板
    const staticContent = `
        <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 25px; flex-wrap: wrap;">
            <div>
                <h3 style="color: #ff6600; margin-bottom: 10px; border-bottom: 1px solid rgba(255, 102, 0, 0.3); padding-bottom: 10px;">
                    <i class="fas fa-building" style="margin-right: 10px;"></i>${companyNames[companyIndex-1]}
                </h3>
                <p style="margin-bottom: 5px;">
                    <strong style="color: #ff8844;">档案编号:</strong> 
                    <span style="color: #ffaa66; font-family: 'Orbitron', sans-serif;">DGC-COMP-${companyIndex.toString().padStart(3, '0')}</span>
                </p>
                <p style="margin-bottom: 15px;">
                    <strong style="color: #ff8844;">创始人:</strong> 
                    <span style="color: #ffaa66;">${founders[companyIndex-1]}</span>
                </p>
            </div>
            <div style="background-color: rgba(255, 102, 0, 0.1); padding: 10px 15px; border-radius: 8px;">
                <p style="margin-bottom: 5px;">
                    <strong style="color: #ff8844;">创建日期:</strong> 
                    <span style="color: #ffaa66;">3025-${Math.floor(Math.random() * 12 + 1).toString().padStart(2, '0')}-${Math.floor(Math.random() * 28 + 1).toString().padStart(2, '0')}</span>
                </p>
                <p>
                    <strong style="color: #ff8844;">档案状态:</strong> 
                    <span style="color: #00ff00; font-family: 'Orbitron', sans-serif;">
                        <i class="fas fa-check-circle"></i> 已归档 • 安全
                    </span>
                </p>
            </div>
        </div>
        
        <div style="background: linear-gradient(90deg, rgba(255, 102, 0, 0.1), transparent); padding: 15px; border-left: 3px solid #ff6600; margin-bottom: 25px; border-radius: 0 8px 8px 0;">
            <h4 style="color: #ff6600; margin-bottom: 10px; display: flex; align-items: center;">
                <i class="fas fa-file-alt" style="margin-right: 10px;"></i>档案摘要
            </h4>
            <p style="color: #ffaa66; line-height: 1.7;">${companyDescriptions[companyIndex-1]}</p>
        </div>
        
        <div style="margin-bottom: 25px;">
            <h4 style="color: #ff6600; margin-bottom: 15px; display: flex; align-items: center;">
                <i class="fas fa-history" style="margin-right: 10px;"></i>历史时间线
            </h4>
            <div style="position: relative; padding-left: 20px;">
                <div style="position: absolute; left: 0; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, #ff6600, transparent);"></div>
                <ul style="padding-left: 20px; color: #ffaa66; list-style: none;">
                    <li style="margin-bottom: 12px; position: relative;">
                        <div style="position: absolute; left: -28px; top: 5px; width: 10px; height: 10px; background: #ff6600; border-radius: 50%;"></div>
                        <strong>创立时期:</strong> 2980-2990年<br>
                        <span style="font-size: 0.9rem; color: #cc5500;">公司初创阶段，确立核心技术方向</span>
                    </li>
                    <li style="margin-bottom: 12px; position: relative;">
                        <div style="position: absolute; left: -28px; top: 5px; width: 10px; height: 10px; background: #ff6600; border-radius: 50%;"></div>
                        <strong>扩张阶段:</strong> 2990-3010年<br>
                        <span style="font-size: 0.9rem; color: #cc5500;">技术商业化，市场份额快速增长</span>
                    </li>
                    <li style="margin-bottom: 12px; position: relative;">
                        <div style="position: absolute; left: -28px; top: 5px; width: 10px; height: 10px; background: #ff6600; border-radius: 50%;"></div>
                        <strong>稳定运营:</strong> 3010-3025年<br>
                        <span style="font-size: 0.9rem; color: #cc5500;">成为行业领导者，持续技术创新</span>
                    </li>
                    <li style="position: relative;">
                        <div style="position: absolute; left: -28px; top: 5px; width: 10px; height: 10px; background: #00ff00; border-radius: 50%; box-shadow: 0 0 10px #00ff00;"></div>
                        <strong>当前状态:</strong> 正常运营中<br>
                        <span style="font-size: 0.9rem; color: #00ff00;">稳定贡献城市GDP，持续研发投入</span>
                    </li>
                </ul>
            </div>
        </div>
        
        <div style="background: rgba(0, 0, 0, 0.3); padding: 20px; border: 1px solid rgba(255, 102, 0, 0.2); border-radius: 8px; margin-top: 20px;">
            <h4 style="color: #ff6600; margin-bottom: 10px; display: flex; align-items: center;">
                <i class="fas fa-info-circle" style="margin-right: 10px;"></i>访问说明
            </h4>
            <p style="color: #ffaa66; margin-bottom: 10px;">此档案为安全级别内容，采用静态加密展示技术。</p>
            <p style="color: #cc5500; font-size: 0.9rem; font-style: italic;">
                <i class="fas fa-shield-alt" style="margin-right: 8px;"></i>
                提示: 此界面内容已通过CH-AI系统加密，仅限权限访问。所有信息均为只读状态。
            </p>
        </div>
    `;
    
    staticDetailContent.innerHTML = staticContent;
    
    console.log(`为公司 #${companyIndex} 生成静态详情内容`);
}

// 绑定菜单点击事件
function setupMenuEvents() {
    console.log("设置菜单事件");
    
    // 绑定进入系统按钮
    if (menuButton) {
        menuButton.addEventListener('click', openTimescreen);
        console.log("菜单按钮事件已绑定");
    }
    
    // 绑定时报界面按钮
    if (timescreenBackButton) {
        timescreenBackButton.addEventListener('click', closeToLoading);
    }
    
    // 绑定数据库界面按钮
    if (databaseBackButton) {
        databaseBackButton.addEventListener('click', closeToLoading);
    }
    
    // 绑定地图界面按钮
    if (mapBackButton) {
        mapBackButton.addEventListener('click', closeToLoading);
    }
    
    // 绑定公司历史界面按钮
    if (openCompanyHistoryButton) {
        openCompanyHistoryButton.addEventListener('click', openCompanyHistory);
    }
    if (companyHistoryBackButton) {
        companyHistoryBackButton.addEventListener('click', backToDatabase);
    }
    
    // 绑定公司详情界面按钮
    if (companyDetailBackButton) {
        companyDetailBackButton.addEventListener('click', backToCompanyHistory);
    }
    
    // 绑定底部导航栏点击事件
    navItems.forEach(item => {
        item.addEventListener('click', function() {
            const targetScreen = this.dataset.target;
            if (targetScreen && activeScreen !== targetScreen) {
                switchToScreen(targetScreen);
            }
        });
    });
    
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
        if (e.key === 'Escape') {
            if (activeScreen === 'company-history') {
                backToDatabase();
            } else if (activeScreen === 'company-detail') {
                backToCompanyHistory();
            } else if (activeScreen !== 'loading') {
                closeToLoading();
            }
        }
        
        // M键打开时报（如果在加载界面）
        if (e.key === 'm' && activeScreen === 'loading' && menuButton.style.opacity === '1') {
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
        
        // 左右箭头键切换界面（在主界面时）
        if (activeScreen === 'timescreen' || activeScreen === 'database' || activeScreen === 'map') {
            if (e.key === 'ArrowLeft') {
                // 切换到上一个界面
                const newIndex = (currentScreenIndex - 1 + screens.length) % screens.length;
                switchToScreen(screens[newIndex].id);
            } else if (e.key === 'ArrowRight') {
                // 切换到下一个界面
                const newIndex = (currentScreenIndex + 1) % screens.length;
                switchToScreen(screens[newIndex].id);
            }
        }
        
        // 数字键1-3快速切换到对应界面
        if (activeScreen !== 'loading') {
            if (e.key === '1') switchToScreen('timescreen');
            if (e.key === '2') switchToScreen('database');
            if (e.key === '3') switchToScreen('map');
        }
    });
}            // 启动加载过程
            function startLoading() {
                console.log("开始加载过程");
                
                // 创建标题字母
                createTitleLetters();
                enhanceTitleAnimation();
                
                // 初始化时立即触发一次故障效果
                setTimeout(() => {
                    const subtitle = document.querySelector('.subtitle');
                    if (subtitle) triggerLoadingGlitch(subtitle);
                }, 500);
                
                setTimeout(() => {
                    if (loadingText) {
                        loadingText.textContent = loadingStages[0].text;
                    }
                    updateProgressBar(loadingStages[0].percent);
                }, 800);
            }
            
            // 随机全局故障效果
            function setupRandomEffects() {
                // 加载界面的随机故障效果
                const loadingInterval = setInterval(() => {
                    if (activeScreen === 'loading' && !isLoaded) {
                        if (Math.random() < 0.3) {
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
                    if (Math.random() < 0.2 && activeScreen !== 'loading') {
                        const elements = [
                            document.querySelector('.menu-title'),
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
                
                // 添加交互功能
                initMouseFollow();
                initParallaxEffect();
                
                // 设置菜单事件
                setupMenuEvents();
                setupKeyboardShortcuts();
                
                // 初始化底部导航栏滑动功能
                initBottomNavSwipe();
                
                // 开始加载过程
                startLoading();
                
                // 使用加载模拟
                simulateLoading();
                
                // 设置随机效果
                setupRandomEffects();
                
                // 增强内容显示
                enhanceContentReveal();
                
                updateStatus("模式激活");
                console.log("系统初始化完成");
            }
            
            // 开始初始化
            initialize();
        });
    </script>
</body>
</html>
