# Mengangchengnline.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ISC</title>

<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@900&display=swap" rel="stylesheet">

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :root {
    --accent-cyan: #00f3ff;
  }

  body, html {
    height: 100%;
    width: 100%;
    font-family: 'Microsoft YaHei', 'PingFang SC', sans-serif;
    overflow: hidden;
  }

  #global-bg-canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 0;
    pointer-events: none;
  }

  #initial-boot-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: #000000;
    z-index: 10000;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-image: linear-gradient(rgba(255, 165, 0, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 165, 0, 0.05) 1px, transparent 1px);
    background-size: 30px 30px;
  }

  .boot-top-text {
    position: absolute;
    top: 15%;
    color: #FFA500;
    font-size: 1.6vw;
    font-weight: 900;
    letter-spacing: 4px;
    text-shadow: 0 0 15px #FFA500;
    font-family: 'Orbitron', 'Microsoft YaHei', sans-serif;
  }

  .boot-mid-container {
    position: relative;
    width: 100%;
    height: 100px;
    margin-bottom: 30px;
  }

  .boot-text {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    color: #FFA500;
    font-size: 1.8rem;
    font-weight: 900;
    letter-spacing: 3px;
    white-space: nowrap;
    -webkit-box-reflect: below 2px linear-gradient(transparent 40%, rgba(255, 255, 255, 0.6));
  }

  .boot-text.typing {
    left: 20%;
    text-shadow: 0 0 15px #FFA500, 0 0 30px #FFA500;
  }

  .boot-text.teleporting {
    animation: teleportAnim 0.3s forwards;
  }

  @keyframes teleportAnim {
    0% { left: 20%; transform: translateY(-50%); text-shadow: 0 0 15px #FFA500, 0 0 30px #FFA500; opacity: 1; }
    49% { left: 20%; transform: translateY(-50%); text-shadow: -15px 0 20px #FFA500, 15px 0 20px #8B0000; opacity: 0.8; }
    50% { left: 50%; transform: translate(-50%, -50%); text-shadow: -30px 0 30px #FFA500, 30px 0 30px #8B0000; opacity: 0.4; }
    90% { left: 50%; transform: translate(-50%, -50%); text-shadow: -10px 0 20px #FFA500, 10px 0 20px #8B0000; opacity: 0.8; }
    100% { left: 50%; transform: translate(-50%, -50%); text-shadow: 0 0 15px #FFA500, 0 0 30px #FFA500; opacity: 1; }
  }

  .boot-text.final-state {
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0;
    color: #FFA500;
    text-shadow: 0 0 20px #FFA500, 0 0 40px #FFA500, 0 0 60px #FFA500;
    font-size: 2.2rem;
    animation: fadeInText 0.5s ease forwards;
  }

  @keyframes fadeInText {
    to { opacity: 1; }
  }

  .boot-bar-container {
    width: 45vw;
    height: 25px;
    border: 2px solid #FFA500;
    box-shadow: 0 0 15px rgba(255, 165, 0, 0.4), inset 0 0 10px rgba(255, 165, 0, 0.2);
    position: relative;
    background: rgba(0, 0, 0, 0.5);
    margin-bottom: 50px;
  }

  .boot-bar-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(to right, #FFA500, #8B0000);
    box-shadow: 0 0 15px #FFA500;
  }

  .boot-percentage {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #FFA500;
    font-weight: 900;
    font-size: 1.1rem;
    text-shadow: 0 0 8px #FFA500, 0 0 5px #000000;
    font-family: 'Orbitron', sans-serif;
  }

  #boot-start-btn {
    opacity: 0;
    pointer-events: none;
    padding: 12px 50px;
    font-size: 1.8rem;
    font-weight: 900;
    color: #FFA500;
    text-shadow: 0 0 10px #FFA500;
    background: rgba(255, 165, 0, 0.1);
    border: 2px solid #FFA500;
    box-shadow: 0 0 15px rgba(255, 165, 0, 0.5), inset 0 0 10px rgba(255, 165, 0, 0.2);
    cursor: pointer;
    transition: all 0.3s;
    font-family: 'Orbitron', sans-serif;
    letter-spacing: 4px;
  }

  #boot-start-btn.show {
    opacity: 1;
    pointer-events: auto;
    animation: btnPulse 1.5s infinite alternate;
  }

  #boot-start-btn:hover {
    background: #FFA500;
    color: #000000;
    box-shadow: 0 0 25px rgba(255, 165, 0, 1);
  }

  @keyframes btnPulse {
    from { box-shadow: 0 0 15px rgba(255, 165, 0, 0.5), inset 0 0 10px rgba(255, 165, 0, 0.2); }
    to { box-shadow: 0 0 25px rgba(255, 165, 0, 0.8), inset 0 0 20px rgba(255, 165, 0, 0.5); }
  }

  .navbar {
    height: calc(100vh / 15);
    background-color: #FF8C00;
    display: flex;
    align-items: center;
    width: 100%;
    position: relative;
    z-index: 100;
  }

  .isc-logo {
    width: 10%;
    height: 100%;
    color: #000000;
    font-family: 'Orbitron', sans-serif;
    font-size: 2.2vw;
    font-weight: 900;
    display: flex;
    justify-content: center;
    align-items: center;
    letter-spacing: 2px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .isc-logo:hover {
    color: #ffffff;
    text-shadow: 0 0 10px #ffffff;
  }

  .spacer {
    width: 10%;
  }

  .nav-links {
    display: flex;
    gap: 3vw;
    align-items: center;
    height: 100%;
  }

  .nav-links > a {
    text-decoration: none;
    color: #000000;
    font-weight: 900;
    font-size: 1.1rem;
    transition: all 0.3s ease;
    cursor: pointer;
    line-height: calc(100vh / 15);
  }

  .nav-links > a:hover {
    color: #ffffff;
    text-shadow: 0 0 8px #ffffff;
  }

  .sentry-container {
    margin-left: auto;
    margin-right: 2vw;
  }

  .sentry-eye {
    width: 32px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    cursor: pointer;
  }

  .sentry-eye svg { overflow: visible; }

  .sentry-ring {
    fill: none;
    stroke: #333;
    stroke-width: 1.5;
    stroke-dasharray: 10 15;
    transform-origin: center;
    transition: all 0.4s;
  }

  .sentry-rhombus {
    fill: #FFA500;
    stroke: #222;
    stroke-width: 1.5;
    opacity: 1;
    transform-origin: center;
    transition: all 0.3s;
  }

  .sentry-glint {
    fill: #ffffff;
    opacity: 1;
    transform-origin: center;
    transition: cx 0.15s ease, cy 0.15s ease, fill 0.3s, r 0.3s;
  }

  .sentry-eye.idle .sentry-ring { animation: ringSpinSlow 12s linear infinite; }
  .sentry-eye.idle .sentry-rhombus { opacity: 1; }
  .sentry-eye.idle .sentry-glint { opacity: 1; }

  .sentry-eye.processing .sentry-ring {
    stroke: var(--accent-cyan);
    stroke-width: 3;
    stroke-dasharray: 60 0;
    animation: ringSpinFast 0.5s linear infinite;
  }
  .sentry-eye.processing .sentry-rhombus {
    fill: #ffffff;
    stroke: var(--accent-cyan);
    animation: rhombusPulse 0.2s infinite alternate;
  }
  .sentry-eye.processing .sentry-glint {
    fill: var(--accent-cyan);
    r: 2;
    opacity: 1;
  }

  @keyframes ringSpinSlow { 100% { transform: rotate(360deg); } }
  @keyframes ringSpinFast { 100% { transform: rotate(360deg); } }
  @keyframes rhombusPulse { 0% { transform: scale(1); } 100% { transform: scale(1.3); } }

  .sub-panel {
    position: fixed;
    top: calc(100vh / 15);
    left: 0;
    width: 100vw;
    height: 0;
    background-color: #000000;
    z-index: 90;
    overflow: hidden;
    transition: height 0.4s cubic-bezier(0.25, 1, 0.5, 1);
    border-bottom: 2px solid transparent;
  }

  .sub-panel.active {
    height: 50vh;
    border-bottom: 2px solid #FF8C00;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  }

  .close-btn {
    position: absolute;
    top: 3vh;
    right: 3vw;
    color: #FF8C00;
    font-family: 'Orbitron', sans-serif;
    font-size: 1.2rem;
    font-weight: 900;
    cursor: pointer;
    display: flex;
    align-items: center;
    transition: all 0.3s ease;
    z-index: 10;
  }

  .close-btn:hover {
    color: #ffffff;
    text-shadow: 0 0 10px #ffffff;
  }

  .close-btn span {
    font-size: 2rem;
    margin-right: 8px;
    line-height: 1;
  }

  .panel-content {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: flex-start;
    padding-left: 10vw;
    padding-top: 5vh;
    padding-bottom: 5vh;
  }

  #panel-wiki .panel-content {
    display: grid;
    grid-template-rows: repeat(5, 1fr);
    grid-auto-flow: column;
    column-gap: 8vw;
    align-items: center;
    justify-content: start;
  }

  .panel-link {
    color: #ffffff;
    text-decoration: none;
    font-size: 1.6rem;
    font-weight: bold;
    letter-spacing: 3px;
    transition: all 0.3s ease;
    border-left: 0px solid transparent;
  }

  .panel-link:hover {
    color: #FF8C00;
    text-shadow: 0 0 15px #FF8C00;
    padding-left: 20px;
    border-left: 4px solid #FF8C00;
  }

  .main-content {
    height: calc(100vh - (100vh / 15));
    width: 100%;
    overflow-y: auto;
    background-color: transparent;
    box-shadow: inset 0px -20px 40px rgba(0, 0, 0, 0.05);
    position: relative;
    z-index: 10;
  }

  .scroll-section {
    width: 100%;
    min-height: 100%;
    padding: 5% 10%;
    display: flex;
    flex-direction: column;
  }

  .gif-section {
    justify-content: center;
    align-items: center;
  }

  .gif-container {
    width: 80vw;
    height: 80vh;
    background-color: rgba(255, 140, 0, 0.05);
    border: 2px dashed rgba(255, 140, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .gif-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .content-section {
    justify-content: flex-start;
  }

  .section-title {
    width: 10vw;
    color: #FF8C00;
    font-size: 1.8vw;
    font-weight: 900;
    border-bottom: 2px solid #FF8C00;
    padding-bottom: 10px;
    margin-bottom: 40px;
    white-space: nowrap;
  }

  .cards-wrapper {
    display: flex;
    gap: 3vw;
    align-items: flex-start;
    flex-wrap: wrap;
  }

  .card-item {
    background: rgba(0, 0, 0, 0.7);
    border: 1px solid #FF8C00;
    color: #ffffff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
    font-weight: bold;
    box-shadow: 0 0 10px rgba(255, 140, 0, 0.2);
    transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
    cursor: pointer;
  }

  .card-item:hover {
    box-shadow: 0 0 20px rgba(255, 140, 0, 0.6);
  }

  .card-square {
    width: 25vw;
    height: 25vw;
  }

  .card-vertical {
    width: 10vw;
    height: 25vw;
  }

  .card-item.expanded {
    width: 80vw;
    height: 50vh;
    box-shadow: 0 0 25px rgba(255, 140, 0, 0.8);
    z-index: 10;
  }

  .about-text-box {
    width: 50vw;
    min-height: 20vh;
    background: rgba(0, 0, 0, 0.7);
    border: 1px solid #FF8C00;
    color: #ffffff;
    padding: 20px;
    font-size: 1.2rem;
    line-height: 1.8;
    transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
    cursor: pointer;
  }

  .about-text-box.expanded {
    width: 80vw;
    min-height: 60vh;
    box-shadow: 0 0 25px rgba(255, 140, 0, 0.8);
  }

  .dir-main-title {
    height: 12.5vh;
    line-height: 12.5vh;
    font-size: 3.5rem;
    font-weight: 900;
    color: #000000;
    white-space: nowrap;
    margin-bottom: 2vh;
  }

  .dir-catalog-box {
    display: inline-block;
    font-size: 2rem;
    font-weight: bold;
    color: #FF8C00;
    padding: 10px 30px;
    border: 2px solid #FF8C00;
    box-shadow: 0 0 15px rgba(255, 140, 0, 0.6), inset 0 0 10px rgba(255, 140, 0, 0.2);
    margin-bottom: 5vh;
  }

  .dir-content-wrapper {
    margin-bottom: 5vh;
  }

  .dir-sub-title {
    font-size: 1.8rem;
    font-weight: bold;
    color: #333333;
  }

  .dir-divider {
    width: 100%;
    height: 2px;
    background-color: #FFD700;
    margin: 15px 0;
    box-shadow: 0 0 8px rgba(255, 215, 0, 0.8);
  }

  .dir-body-text {
    font-size: 1.2rem;
    line-height: 1.8;
    color: #00A2E8;
    font-weight: bold;
  }

  #loading-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: #000000;
    z-index: 9999;
    display: none;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .loading-top-text {
    color: #FFA500;
    font-size: 1.6rem;
    font-weight: 900;
    letter-spacing: 3px;
    text-shadow: 0 0 15px #FFA500, 0 0 30px #FFA500;
    margin-bottom: 15px;
    font-family: 'Orbitron', 'Microsoft YaHei', sans-serif;
  }

  .loading-mid-text {
    color: #FFA500;
    font-size: 1.2rem;
    font-weight: 900;
    text-shadow: 0 0 10px #FFA500, 0 0 20px #FFA500;
    margin-bottom: 30px;
    letter-spacing: 5px;
  }

  .loading-bar-container {
    width: 40vw;
    height: 30px;
    border: 2px solid #FFA500;
    box-shadow: 0 0 15px rgba(255, 165, 0, 0.8), inset 0 0 10px rgba(255, 165, 0, 0.3);
    position: relative;
    background-color: rgba(0, 0, 0, 0.3);
  }

  .loading-bar-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(to right, #FFA500, #8B0000);
    background-size: 40vw 100%;
    box-shadow: 0 0 10px rgba(255, 165, 0, 0.6);
  }

  .loading-percentage {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #FFA500;
    font-weight: 900;
    font-size: 1rem;
    text-shadow: 0 0 8px #FFA500, 0 0 5px #000000;
    z-index: 2;
    font-family: 'Orbitron', sans-serif;
  }

  .dh-layout-wrapper {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: transparent;
      z-index: 50;
      overflow: hidden;
  }

  .dh-layout-grid {
      display: grid;
      grid-template-columns: 3fr 6fr 1fr;
      width: 100%;
      height: 100%;
      position: relative;
      font-family: 'Arial Black', Impact, sans-serif;
  }

  .dh-col-left {
      display: flex;
      flex-direction: column-reverse;
      justify-content: space-evenly;
      align-items: center;
      padding-right: 1.5vw;
      overflow: hidden;
      z-index: 1;
  }

  .dh-col-left span {
      font-size: 12vh;
      line-height: 0.8;
      color: #000;
      text-transform: uppercase;
      transform: rotate(-90deg);
      display: inline-block;
      font-weight: 900;
  }

  .dh-col-mid {
      border-left: 1px solid #000;
      border-right: 1px solid #000;
      padding: 0 1.5vw;
      background-color: transparent;
      position: relative;
      overflow: hidden;
  }

  .dh-col-mid img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      display: block;
  }

  .dh-col-right {
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      padding: 3vh 0 3vh 1.5vw;
      font-family: Arial, Helvetica, sans-serif;
  }

  .dh-right-wrapper {
      display: flex;
      flex-direction: column;
      align-items: center;
      height: 100%;
      width: 2vw;
  }

  .dh-barcode {
      width: 1vw;
      height: 12vh;
      background: repeating-linear-gradient(
          to bottom,
          #000, #000 2px, transparent 2px, transparent 4px,
          #000 4px, #000 6px, transparent 6px, transparent 8px
      );
      margin-bottom: 5vh;
  }

  .dh-right-orange-block {
      width: 100%;
      height: 15vh;
      background-color: #f08323;
      margin: 4vh 0;
  }

  .dh-dots {
      margin-top: auto;
      display: flex;
      flex-direction: column;
      gap: 0.8vh;
  }

  .dh-dot {
      width: 1.2vh;
      height: 1.2vh;
      background-color: #000;
      border-radius: 50%;
  }

  .dh-overlap-container {
      position: absolute;
      top: 32vh;
      left: 2vw;
      width: 25vw;
      max-width: 85vw;
      z-index: 10;
  }

  .dh-teal-box {
      background-color: #f08323;
      width: 100%;
      padding: 2vh 3vw;
      color: #fff;
      position: relative;
      z-index: 2;
  }

  .dh-teal-box h1 {
      font-size: 5vh;
      line-height: 0.95;
      margin-bottom: 0;
  }

  .dh-overlap-lightblue {
      position: absolute;
      top: 50%;
      right: -2vw;
      transform: translateY(-50%);
      width: 3vw;
      height: 9vh;
      background-color: #87ceeb;
      z-index: 1;
  }

  .inner-link-container {
    margin-top: 4vh;
    text-align: left;
  }

  .inner-link-btn {
    display: inline-block;
    font-size: 1.2rem;
    font-weight: bold;
    color: #FF8C00;
    text-decoration: none;
    padding: 10px 20px;
    border: 1px solid #FF8C00;
    background: rgba(0, 0, 0, 0.8);
    transition: all 0.3s ease;
    box-shadow: 0 0 10px rgba(255, 140, 0, 0.3);
    cursor: pointer;
  }

  .inner-link-btn:hover {
    background: #FF8C00;
    color: #000;
    box-shadow: 0 0 20px rgba(255, 140, 0, 0.8);
  }

  .editable-content {
    width: 100%;
    min-height: 40vh;
    background: rgba(249, 249, 249, 0.85);
    border: 1px dashed #FF8C00;
    padding: 20px;
    font-size: 1.2rem;
    color: #333;
    line-height: 1.8;
    outline: none;
    transition: all 0.3s ease;
  }

  .osc-bounding-box {
      width: 700px;
      height: 420px;
      position: relative;
      margin-left: 10%;
      margin-bottom: 5%;
      cursor: pointer;
  }

  .oscilloscope {
      --panel-bg: #d0cec5;
      --panel-dark: #b8b6ad;
      --screen-bezel: #8c9085;
      --screen-crt: #113311;
      --text-color: #2b2b2b;
      --knob-base: #e6e6e6;
      --knob-dark: #b3b3b3;
      --led-off: #4a1515;
      --led-on: #ff3333;

      transform: scale(0.7);
      transform-origin: top left;
      position: absolute;
      top: 0;
      left: 0;
      
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.5s ease;

      width: 1000px;
      height: 600px;
      background: linear-gradient(135deg, var(--panel-bg) 0%, var(--panel-dark) 100%);
      border-radius: 12px;
      box-shadow: 
          inset 0 0 15px rgba(255,255,255,0.8),
          inset 0 0 50px rgba(0,0,0,0.1),
          0 20px 50px rgba(0,0,0,0.8),
          0 0 0 4px #888,
          0 0 0 10px #333;
      display: flex;
      padding: 20px;
      box-sizing: border-box;
      border: 1px solid #fff;
      font-family: 'Arial', sans-serif;
      user-select: none;
  }

  .oscilloscope.revealed {
      opacity: 1;
      pointer-events: auto;
  }

  .screw {
      width: 12px;
      height: 12px;
      border-radius: 50%;
      background: linear-gradient(145deg, #ccc, #777);
      position: absolute;
      box-shadow: inset 0 0 2px #000, 0 1px 1px rgba(255,255,255,0.8);
  }
  .screw::after {
      content: '';
      position: absolute;
      top: 5px; left: 2px; right: 2px; height: 1.5px;
      background: #333;
      transform: rotate(45deg);
  }
  .screw.tl { top: 10px; left: 10px; }
  .screw.tr { top: 10px; right: 10px; }
  .screw.bl { bottom: 10px; left: 10px; }
  .screw.br { bottom: 10px; right: 10px; }

  .panel {
      display: flex;
      flex-direction: column;
      position: relative;
  }
  .left-panel { width: 25%; border-right: 2px solid rgba(0,0,0,0.1); padding-right: 15px; }
  .center-panel { width: 50%; display: flex; justify-content: center; align-items: center; }
  .right-panel { width: 25%; border-left: 2px solid rgba(255,255,255,0.5); padding-left: 15px; }

  .section-box {
      border: 1px solid rgba(0,0,0,0.2);
      border-top: 1px solid rgba(255,255,255,0.8);
      border-left: 1px solid rgba(255,255,255,0.8);
      margin-bottom: 20px;
      padding: 15px 10px;
      position: relative;
      border-radius: 4px;
  }

  .osc-section-title {
      position: absolute;
      top: -8px;
      left: 10px;
      background: var(--panel-bg);
      padding: 0 5px;
      font-size: 12px;
      font-weight: bold;
      color: var(--text-color);
      letter-spacing: 1px;
  }

  .knob-container {
      width: 120px;
      height: 120px;
      margin: 20px auto;
      position: relative;
  }
   
  .dial-scale {
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 50%;
  }

  .scale-mark {
      position: absolute;
      width: 2px;
      height: 6px;
      background-color: #333;
  }
   
  .scale-text {
      position: absolute;
      font-size: 11px;
      font-weight: bold;
      color: #222;
      text-shadow: 1px 1px 0 rgba(255,255,255,0.5);
  }

  .knob {
      width: 70px;
      height: 70px;
      background: radial-gradient(circle at 50% 30%, var(--knob-base) 0%, var(--knob-dark) 80%);
      border-radius: 50%;
      position: absolute;
      top: 25px;
      left: 25px;
      box-shadow: 
          0 8px 10px rgba(0,0,0,0.4),
          inset 0 2px 3px rgba(255,255,255,0.8),
          inset 0 -2px 5px rgba(0,0,0,0.2);
      cursor: pointer;
      transition: transform 0.1s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 10;
      display: flex;
      justify-content: center;
      touch-action: none;
  }
   
  .knob::before {
      content: '';
      position: absolute;
      top: 2px; left: 2px; right: 2px; bottom: 2px;
      border-radius: 50%;
      background: repeating-conic-gradient(
          from 0deg,
          rgba(0,0,0,0.1) 0deg, rgba(0,0,0,0.1) 5deg,
          transparent 5deg, transparent 10deg
      );
      mask-image: radial-gradient(circle, transparent 60%, black 100%);
      -webkit-mask-image: radial-gradient(circle, transparent 60%, black 100%);
  }

  .knob-pointer {
      width: 4px;
      height: 25px;
      background: #222;
      position: absolute;
      top: 5px;
      border-radius: 2px;
      box-shadow: 1px 1px 1px rgba(255,255,255,0.5);
  }

  .screen-bezel {
      width: 420px;
      height: 350px;
      background: var(--screen-bezel);
      border-radius: 20px;
      box-shadow: 
          inset 0 10px 20px rgba(0,0,0,0.6),
          inset 0 -5px 15px rgba(255,255,255,0.4),
          0 5px 15px rgba(0,0,0,0.3);
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
  }

  .crt-container {
      width: 360px;
      height: 290px;
      background: var(--screen-crt);
      border-radius: 10px;
      position: relative;
      overflow: hidden;
      box-shadow: inset 0 0 30px #000;
  }

  #noiseCanvas {
      width: 100%;
      height: 100%;
      image-rendering: pixelated;
      opacity: 0.85;
      filter: contrast(1.5) brightness(1.2);
  }

  .crt-overlay {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: 
          linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), 
          linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
      background-size: 100% 4px, 6px 100%;
      pointer-events: none;
      z-index: 2;
  }

  .graticule {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background-image: 
          linear-gradient(rgba(50, 255, 50, 0.3) 1px, transparent 1px),
          linear-gradient(90deg, rgba(50, 255, 50, 0.3) 1px, transparent 1px);
      background-size: 36px 29px;
      background-position: center center;
      pointer-events: none;
      z-index: 3;
      box-shadow: inset 0 0 50px rgba(0,0,0,0.8);
  }
  .graticule::after {
      content: '';
      position: absolute;
      top: 50%; left: 0; right: 0; height: 1px;
      background: rgba(50, 255, 50, 0.5);
  }
  .graticule::before {
      content: '';
      position: absolute;
      left: 50%; top: 0; bottom: 0; width: 1px;
      background: rgba(50, 255, 50, 0.5);
  }

  .crt-glare {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: radial-gradient(circle at 50% 50%, rgba(100, 255, 100, 0.1) 0%, transparent 70%);
      z-index: 4;
      pointer-events: none;
  }

  .brand-logo {
      text-align: right;
      font-size: 24px;
      font-weight: 900;
      letter-spacing: 2px;
      margin-bottom: 20px;
      color: #222;
      text-shadow: 1px 1px 0px rgba(255,255,255,0.5);
  }

  .extra-controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
      border-top: 1px inset rgba(0,0,0,0.1);
      padding-top: 25px;
  }

  .indicator-wrapper {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 12px;
      font-weight: bold;
  }
  .led {
      width: 14px;
      height: 14px;
      border-radius: 50%;
      background-color: var(--led-off);
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.5), 0 1px 1px rgba(255,255,255,0.5);
      transition: all 0.1s;
  }
  .led.blink {
      background-color: var(--led-on);
      box-shadow: inset 0 0 2px #fff, 0 0 10px var(--led-on), 0 0 20px var(--led-on);
  }

  .btn-noise-wrapper {
      padding: 6px;
      background: #a0a099;
      border-radius: 50%;
      box-shadow: inset 0 3px 6px rgba(0,0,0,0.6), 0 1px 2px rgba(255,255,255,0.8);
      display: inline-block;
  }
   
  .btn-noise {
      width: 48px;
      height: 48px;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(to bottom, #eaeaea 0%, #bebebe 100%);
      border: 1px solid #777;
      border-bottom: 4px solid #666;
      border-radius: 50%;
      font-weight: bold;
      font-size: 11px;
      color: #333;
      cursor: pointer;
      box-shadow: inset 0 1px 2px rgba(255,255,255,0.9), 0 3px 6px rgba(0,0,0,0.5);
      text-transform: uppercase;
      text-shadow: 1px 1px 0 rgba(255,255,255,0.6);
      transition: all 0.1s;
  }
   
  .btn-noise:active {
      transform: translateY(3px);
      border-bottom: 1px solid #666;
      background: linear-gradient(to bottom, #d0d0d0 0%, #a0a0a0 100%);
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.5), 0 1px 1px rgba(0,0,0,0.2);
  }
   
  .btn-noise.active {
      background: linear-gradient(to bottom, #a0d8a0 0%, #60a860 100%);
      border-bottom: 4px solid #408040;
      color: #003300;
      text-shadow: 1px 1px 0 rgba(255,255,255,0.4);
  }
   
  .btn-noise.active:active {
      transform: translateY(3px);
      border-bottom: 1px solid #408040;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.5), 0 1px 1px rgba(0,0,0,0.2);
  }

  .bnc {
      width: 30px; height: 30px;
      border-radius: 50%;
      background: #aaa;
      margin: 10px auto;
      border: 4px solid #ddd;
      box-shadow: 0 5px 5px rgba(0,0,0,0.5), inset 0 0 10px #000;
      display: flex; justify-content: center; align-items: center;
  }
  .bnc-inner {
      width: 12px; height: 12px;
      border-radius: 50%; background: #222;
      border: 2px solid #fff;
  }

  @media (max-width: 768px) {
      .dh-teal-box h1 { font-size: 2.8vh; white-space: nowrap; }
      .dh-col-left span { font-size: 6.4vh; font-weight: 900; -webkit-text-stroke: 1.5px #000; }
      
      .dh-overlap-container { width: max-content; min-width: 33.33vw; top: 34vh; left: 5vw; }
      
      .dh-overlap-lightblue {
          top: 1vh !important; 
          transform: none !important;
          right: -2.5vw !important;
          height: 5.5vh !important;
      }
      .dh-right-wrapper { width: 3.2vw; }
      .dh-barcode { width: 1.6vw; }

      .boot-bar-container, .loading-bar-container { width: 64vw; height: 20px; }
      .loading-bar-fill { background-size: 64vw 100%; }
      .boot-top-text, .loading-top-text { font-size: 3.2vw; text-align: center; padding: 0 8px; line-height: 1.5; }
      .loading-mid-text { font-size: 0.8rem; }
      .boot-mid-container { height: 64px; }
      .boot-text { font-size: 0.96rem; }
      .boot-text.final-state { font-size: 1.2rem; }
      .boot-percentage, .loading-percentage { font-size: 0.88rem; }
      #boot-start-btn { padding: 10px 40px; font-size: 1.44rem; }

      .navbar { justify-content: space-between; height: calc(100vh / 18.75); }
      .isc-logo { width: auto; font-size: 4vw; padding-left: 3.2vw; flex: 0 0 auto; }
      .spacer { display: none; }
      .nav-links { flex: 1; justify-content: space-evenly; gap: 1.6vw; padding: 0 1.6vw; width: auto; }
      .nav-links > a { font-size: 2.8vw; white-space: nowrap; line-height: calc(100vh / 18.75); }
      .sentry-container { margin-left: 0; margin-right: 3.2vw; flex: 0 0 auto; }
      .sentry-eye { transform: scale(0.68); }

      .sub-panel { top: calc(100vh / 18.75); }
      .sub-panel.active { 
          height: auto; 
          min-height: 40vh; 
          max-height: 64vh; 
          overflow-y: auto; 
          padding-bottom: 3.2vh;
      }
      .panel-content, #panel-wiki .panel-content {
          padding: 4.8vh 6.4vw 4vh 6.4vw !important;
          display: grid !important;
          grid-template-columns: repeat(2, 1fr) !important;
          grid-auto-flow: row !important;
          grid-auto-rows: auto !important;
          gap: 3.2vh 3.2vw !important;
          align-content: start !important;
          justify-items: center !important;
      }
      .panel-link { 
          font-size: 0.88rem !important; 
          white-space: nowrap; 
          text-align: left;
          width: 100%;
          padding-left: 8px;
          border-left: 1.5px solid rgba(255, 140, 0, 0.3);
          display: flex;
          align-items: center;
      }
      .close-btn { font-size: 0.96rem; top: 2.4vh; right: 2.4vw; }
      .close-btn span { font-size: 1.6rem; margin-right: 6px; }

      .main-content { height: calc(100vh - (100vh / 18.75)); }
      .scroll-section { padding: 4% 4%; }
      .gif-container { width: 72vw; height: 28vh; }
      .section-title { font-size: 4.8vw; width: auto; display: inline-block; padding-right: 12px; margin-bottom: 32px; }
      
      .cards-wrapper { flex-direction: column; align-items: center; width: 100%; gap: 4vw; }
      .card-item { width: 72vw !important; height: 16vh !important; font-size: 0.96rem; }
      .card-item.expanded { width: 72vw !important; height: 36vh !important; }
      
      .about-text-box { width: 72vw; min-height: 20vh; font-size: 0.96rem; padding: 16px; }
      .about-text-box.expanded { width: 72vw; min-height: 40vh; }

      .dir-main-title { font-size: 1.76rem; margin-top: 4vh; white-space: normal; line-height: 1.2; height: auto; margin-bottom: 2.4vh; }
      .dir-catalog-box { font-size: 0.96rem; padding: 4px 12px; margin-bottom: 2.4vh; border-width: 1.5px; }
      .dir-sub-title { font-size: 1.12rem; }
      .dir-body-text { font-size: 0.96rem; line-height: 1.6; }
      .dir-content-wrapper { margin-bottom: 4vh; }
      
      .inner-link-btn { font-size: 0.96rem !important; padding: 6px 15px !important; white-space: nowrap; }
      .editable-content { font-size: 0.96rem; min-height: 32vh; padding: 16px; }

      .osc-bounding-box { 
          width: 100vw; 
          height: 176px; 
          margin-left: 0; 
          display: flex; 
          justify-content: center; 
          overflow: visible;
      }
      .oscilloscope {
          left: 50%;
          transform: translateX(-50%) scale(0.256) !important;
          transform-origin: top center;
      }
  }
</style>
</head>
<body>

  <canvas id="global-bg-canvas"></canvas>

  <div id="initial-boot-screen">
    <div class="boot-top-text">采用CH级城市管理AI技术-访问模式</div>
    
    <div class="boot-mid-container">
      <div id="boot-text-anim" class="boot-text"></div>
    </div>

    <div class="boot-bar-container">
      <div class="boot-bar-fill" id="boot-fill"></div>
      <div class="boot-percentage" id="boot-perc">0%</div>
    </div>

    <button id="boot-start-btn">START</button>
  </div>


  <div id="loading-overlay">
    <div class="loading-top-text">采用CH级城市管理AI技术-访问模式</div>
    <div class="loading-mid-text">预加载界面</div>
    <div class="loading-bar-container">
      <div class="loading-bar-fill" id="loading-fill"></div>
      <div class="loading-percentage" id="loading-text">0%</div>
    </div>
  </div>

  <nav class="navbar">
    <div class="isc-logo" id="nav-home">ISC</div>
    <div class="spacer"></div>
    <div class="nav-links">
      <a id="nav-wiki-btn">设定百科</a>
      <a id="nav-sheets-btn">各类设表</a>
      <a id="nav-group-btn">群号获取</a>
      <a href="#" class="nav-trigger" data-dir="thanks" data-title="致谢">致谢</a>
    </div>

    <div class="sentry-container">
      <div class="sentry-eye idle" id="sys-indicator" title="SYSTEM SENTRY" onclick="triggerSentryScan()">
        <svg viewBox="0 0 40 40" width="32" height="32" xmlns="http://www.w3.org/2000/svg">
            <circle class="sentry-ring" cx="20" cy="20" r="15" />
            <polygon class="sentry-rhombus" points="20,10 30,20 20,30 10,20" />
            <circle class="sentry-glint" cx="20" cy="20" r="1.5" />
        </svg>
      </div>
    </div>
  </nav>

  <div id="panel-wiki" class="sub-panel">
    <div class="close-btn" onclick="closeAllPanels()"><span>&times;</span> Close</div>
    <div class="panel-content">
      <a href="#" class="nav-trigger panel-link" data-dir="mengyang">梦羊城</a>
      <a href="#" class="nav-trigger panel-link" data-dir="company">公司</a>
      <a href="#" class="nav-trigger panel-link" data-dir="race">种族</a>
      <a href="#" class="nav-trigger panel-link" data-dir="magic">神秘术</a>
      <a href="#" class="nav-trigger panel-link" data-dir="chronicle">编年史</a>
      
      <a href="#" class="nav-trigger panel-link" data-dir="official-org">官方组织</a>
      <a href="#" class="nav-trigger panel-link" data-dir="civilian-org">民间组织</a>
      <a href="#" class="nav-trigger panel-link" data-dir="corruption">现实腐蚀</a>
      <a href="#" class="nav-trigger panel-link" data-dir="alchemy">炼金术</a>
      <a href="#" class="nav-trigger panel-link" data-dir="god">神</a>
    </div>
  </div>

  <div id="panel-sheets" class="sub-panel">
    <div class="close-btn" onclick="closeAllPanels()"><span>&times;</span> Close</div>
    <div class="panel-content">
      <a href="#" class="nav-trigger panel-link" data-dir="player-sheet">玩家设表</a>
      <a href="#" class="nav-trigger panel-link" data-dir="org-sheet">组织设表</a>
      <a href="#" class="nav-trigger panel-link" data-dir="item-sheet">物品设表</a>
      <a href="#" class="nav-trigger panel-link" data-dir="custom-dungeon">自制副本</a>
    </div>
  </div>

  <div id="panel-group" class="sub-panel">
    <div class="close-btn" onclick="closeAllPanels()"><span>&times;</span> Close</div>
    <div class="panel-content">
      <a href="#" class="nav-trigger panel-link" data-dir="audit-group">审群</a>
      <a href="#" class="nav-trigger panel-link" data-dir="chat-group">水群</a>
      <a href="#" class="nav-trigger panel-link" data-dir="rp-group">戏群</a>
    </div>
  </div>

  <main class="main-content">
    
    <div id="home-view">
      <section class="scroll-section gif-section">
        <div class="gif-container">
          <img src="GIFA1.gif" alt="展示图GIFA1">
        </div>
      </section>

      <section class="scroll-section content-section">
        <h2 class="section-title">城市动态</h2>
        <div class="cards-wrapper">
          <div class="card-item card-square">待输入</div>
          <div class="card-item card-vertical">待输入</div>
          <div class="card-item card-vertical">待输入</div>
          <div class="card-item card-vertical">待输入</div>
        </div>
      </section>

      <section class="scroll-section content-section">
        <h2 class="section-title">关于我们</h2>
        <div class="about-text-box">待输入</div>
      </section>

      <div class="osc-bounding-box">
        <div class="oscilloscope">
            <div class="screw tl"></div>
            <div class="screw tr"></div>
            <div class="screw bl"></div>
            <div class="screw br"></div>

            <div class="panel left-panel">
                <div class="section-box">
                    <div class="osc-section-title">КАНАЛ I (CH1)</div>
                    <div class="knob-container" id="knob1-container">
                        <div class="dial-scale" id="scale1"></div>
                        <div class="knob" id="knob1" data-step="0">
                            <div class="knob-pointer"></div>
                        </div>
                    </div>
                    <div class="bnc"><div class="bnc-inner"></div></div>
                </div>

                <div class="section-box">
                    <div class="osc-section-title">КАНАЛ II (CH2)</div>
                    <div class="knob-container" id="knob2-container">
                        <div class="dial-scale" id="scale2"></div>
                        <div class="knob" id="knob2" data-step="0">
                            <div class="knob-pointer"></div>
                        </div>
                    </div>
                    <div class="bnc"><div class="bnc-inner"></div></div>
                </div>
            </div>

            <div class="panel center-panel">
                <div class="screen-bezel">
                    <div class="crt-container">
                        <canvas id="noiseCanvas"></canvas>
                        <div class="crt-overlay"></div>
                        <div class="graticule"></div>
                        <div class="crt-glare"></div>
                    </div>
                </div>
            </div>

            <div class="panel right-panel">
                <div class="brand-logo">C1-83</div>
                
                <div class="section-box">
                    <div class="osc-section-title">ВРЕМЯ/ДЕЛ (TIME/DIV)</div>
                    <div class="knob-container" id="knob3-container">
                        <div class="dial-scale" id="scale3"></div>
                        <div class="knob" id="knob3" data-step="0">
                            <div class="knob-pointer"></div>
                        </div>
                    </div>
                </div>

                <div class="extra-controls">
                    <div class="indicator-wrapper">
                        <span>СИНХР (SYNC)</span>
                        <div class="led" id="status-led"></div>
                    </div>
                    
                    <div class="btn-noise-wrapper">
                        <button class="btn-noise" id="btn-noise"></button>
                    </div>
                </div>
            </div>
        </div>
      </div>
      </div>

    <div id="directory-view" style="display: none;">
      <section class="scroll-section">
        
        <div id="dir-common-header">
            <div class="dir-main-title" id="dir-dynamic-title">动态标题</div>
            <div class="dir-catalog-box">目录</div>
        </div>

        <div id="dir-content-company" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-1">公司小标题1</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-1" data-title="公司小标题1" data-sync-target="company-sub-1" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入1。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-2">公司小标题2</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-2" data-title="公司小标题2" data-sync-target="company-sub-2" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入2。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-3">公司小标题3</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-3" data-title="公司小标题3" data-sync-target="company-sub-3" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入3。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-4">公司小标题4</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-4" data-title="公司小标题4" data-sync-target="company-sub-4" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入4。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-5">公司小标题5</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-5" data-title="公司小标题5" data-sync-target="company-sub-5" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入5。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-6">公司小标题6</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-6" data-title="公司小标题6" data-sync-target="company-sub-6" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入6。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="company-sub-7">公司小标题7</div>
              <a class="nav-trigger inner-link-btn" data-dir="company-inner-7" data-title="公司小标题7" data-sync-target="company-sub-7" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于公司的正文待输入7。</div>
          </div>
        </div>

        <div id="dir-content-official-org" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-1">官方组织小标题1</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-1" data-title="官方组织小标题1" data-sync-target="official-sub-1" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入1。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-2">官方组织小标题2</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-2" data-title="官方组织小标题2" data-sync-target="official-sub-2" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入2。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-3">官方组织小标题3</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-3" data-title="官方组织小标题3" data-sync-target="official-sub-3" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入3。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-4">官方组织小标题4</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-4" data-title="官方组织小标题4" data-sync-target="official-sub-4" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入4。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-5">官方组织小标题5</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-5" data-title="官方组织小标题5" data-sync-target="official-sub-5" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入5。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-6">官方组织小标题6</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-6" data-title="官方组织小标题6" data-sync-target="official-sub-6" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入6。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="official-sub-7">官方组织小标题7</div>
              <a class="nav-trigger inner-link-btn" data-dir="official-inner-7" data-title="官方组织小标题7" data-sync-target="official-sub-7" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于官方组织的正文待输入7。</div>
          </div>
        </div>

        <div id="dir-content-civilian-org" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-1">民间组织小标题1</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-1" data-title="民间组织小标题1" data-sync-target="civilian-sub-1" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入1。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-2">民间组织小标题2</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-2" data-title="民间组织小标题2" data-sync-target="civilian-sub-2" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入2。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-3">民间组织小标题3</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-3" data-title="民间组织小标题3" data-sync-target="civilian-sub-3" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入3。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-4">民间组织小标题4</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-4" data-title="民间组织小标题4" data-sync-target="civilian-sub-4" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入4。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-5">民间组织小标题5</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-5" data-title="民间组织小标题5" data-sync-target="civilian-sub-5" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入5。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-6">民间组织小标题6</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-6" data-title="民间组织小标题6" data-sync-target="civilian-sub-6" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入6。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-7">民间组织小标题7</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-7" data-title="民间组织小标题7" data-sync-target="civilian-sub-7" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入7。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-8">民间组织小标题8</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-8" data-title="民间组织小标题8" data-sync-target="civilian-sub-8" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入8。</div>
          </div>
          <div class="dir-content-wrapper">
            <div style="display: flex; justify-content: space-between; align-items: center;">
              <div class="dir-sub-title" data-sync-id="civilian-sub-9">民间组织小标题9</div>
              <a class="nav-trigger inner-link-btn" data-dir="civilian-inner-9" data-title="民间组织小标题9" data-sync-target="civilian-sub-9" style="font-size: 1rem; padding: 5px 15px;">进入详情</a>
            </div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于民间组织的正文待输入9。</div>
          </div>
        </div>

        <div id="dir-content-corruption" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">小标题1</div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于现实腐蚀的正文待输入1。</div>
          </div>
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">小标题2</div>
            <div class="dir-divider"></div>
            <div class="dir-body-text">这里是关于现实腐蚀的正文待输入2。</div>
          </div>
          <div class="inner-link-container">
            <a class="nav-trigger inner-link-btn" data-dir="corruption-files">现实腐蚀收容档案</a>
          </div>
        </div>

        <div id="dir-content-corruption-files" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">档案记录</div>
            <div class="dir-divider"></div>
            <div class="editable-content">内容待编辑</div>
          </div>
        </div>

        <div id="dir-content-thanks" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">致谢名单</div>
            <div class="dir-divider"></div>
            <div class="editable-content">内容待编辑</div>
          </div>
        </div>

        <div id="dir-content-company-inner-1" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-2" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-3" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-4" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-5" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-6" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>
        <div id="dir-content-company-inner-7" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div>
          </div>
        </div>

        <div id="dir-content-official-inner-1" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-2" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-3" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-4" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-5" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-6" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-official-inner-7" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>

        <div id="dir-content-civilian-inner-1" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-2" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-3" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-4" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-5" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-6" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-7" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-8" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>
        <div id="dir-content-civilian-inner-9" class="dir-specific-content" style="display: none;">
          <div class="dir-content-wrapper"><div class="dir-sub-title">详细档案</div><div class="dir-divider"></div><div class="editable-content">内容待编辑</div></div>
        </div>

      </section>

      <div id="dir-content-mengyang" class="dir-specific-content dh-layout-wrapper" style="display: none;">
        <div class="dh-layout-grid">
            <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
            <div class="dh-col-mid"><img src="B1.jpg" alt="B1"></div>
            <div class="dh-col-right">
                <div class="dh-right-wrapper">
                    <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                    <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                </div>
            </div>
            <div class="dh-overlap-container">
                <div class="dh-teal-box"><h1>梦羊城</h1></div><div class="dh-overlap-lightblue"></div>
            </div>
        </div>
      </div>

      <div id="dir-content-race" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B2.jpg" alt="B2"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>种族</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-magic" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B3.jpg" alt="B3"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>神秘术</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-chronicle" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B4.jpg" alt="B4"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>编年史</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-alchemy" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B5.jpg" alt="B5"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>炼金术</h1></div><div class="dh-overlap-lightblue"></div>
                  <div class="inner-link-container">
                    <a class="nav-trigger inner-link-btn" data-dir="alchemy-misc">炼金术杂项</a>
                  </div>
              </div>
          </div>
      </div>

      <div id="dir-content-alchemy-misc" class="dir-specific-content" style="display: none;">
        <section class="scroll-section">
          <div class="dir-content-wrapper">
            <div class="dir-sub-title">杂项内容</div>
            <div class="dir-divider"></div>
            <div class="editable-content">内容待编辑</div>
          </div>
        </section>
      </div>

      <div id="dir-content-god" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B6.jpg" alt="B6"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>神</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-player-sheet" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B7.jpg" alt="B7"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>玩家设表</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-org-sheet" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B8.jpg" alt="B8"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>组织设表</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-item-sheet" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B9.jpg" alt="B9"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>物品设表</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-custom-dungeon" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B10.jpg" alt="B10"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>自制副本</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-audit-group" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B11.jpg" alt="B11"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>审群</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-chat-group" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B12.jpg" alt="B12"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>水群</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

      <div id="dir-content-rp-group" class="dir-specific-content dh-layout-wrapper" style="display: none;">
          <div class="dh-layout-grid">
              <div class="dh-col-left"><span>A</span><span>R</span><span>I</span><span>E</span><span>S</span><span>D</span></div>
              <div class="dh-col-mid"><img src="B13.jpg" alt="B13"></div>
              <div class="dh-col-right">
                  <div class="dh-right-wrapper">
                      <div class="dh-barcode"></div><div class="dh-right-orange-block"></div>
                      <div class="dh-dots"><div class="dh-dot"></div><div class="dh-dot"></div><div class="dh-dot"></div></div>
                  </div>
              </div>
              <div class="dh-overlap-container">
                  <div class="dh-teal-box"><h1>戏群</h1></div><div class="dh-overlap-lightblue"></div>
              </div>
          </div>
      </div>

    </div>

  </main>

  <audio id="cd1-audio" src="CD1.mp3" preload="auto"></audio>

  <script>
    (function initDynamicBackground() {
        const bgCanvas = document.getElementById('global-bg-canvas');
        if(!bgCanvas) return;
        const bgCtx = bgCanvas.getContext('2d');
        let cw, ch;

        function resizeBg() {
            cw = bgCanvas.width = window.innerWidth;
            ch = bgCanvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeBg);
        resizeBg();

        class DataBar {
            constructor() {
                this.x = Math.random() * cw;
                this.y = Math.random() * ch;
                this.w = Math.random() * 3 + 1;
                this.h = Math.random() * 100 + 20;
                this.speed = Math.random() * 1.5 + 0.5;
                this.opacity = Math.random() * 0.05 + 0.01;
            }
            update() {
                this.y += this.speed;
                if(this.y > ch) {
                    this.y = -this.h;
                    this.x = Math.random() * cw;
                }
            }
            draw(ctx) {
                ctx.fillStyle = `rgba(0, 0, 0, ${this.opacity})`;
                ctx.fillRect(this.x, this.y, this.w, this.h);
            }
        }
        const dataBars = Array.from({length: 80}, () => new DataBar());

        class Bubble {
            constructor() {
                this.y = Math.random() * window.innerHeight;
                this.isLine1 = Math.random() > 0.5;
                this.driftX = (Math.random() - 0.5) * 40;
                this.speedY = Math.random() * 0.6 + 0.1;
                this.radius = Math.random() * 1.8 + 0.5;
                this.opacity = Math.random() * 0.3 + 0.1;
                this.phase = Math.random() * Math.PI * 2;
            }
            update() {
                this.y -= this.speedY;
                if (this.y < -20) {
                    this.y = ch + 20;
                    this.isLine1 = Math.random() > 0.5;
                    this.driftX = (Math.random() - 0.5) * 40;
                }
            }
            draw(ctx, lineTime) {
                let progress = this.y / ch;
                let baseX = this.isLine1 ? (progress * cw) : (cw - progress * cw);
                
                let env = Math.sin(progress * Math.PI);
                let offset = Math.sin(progress * Math.PI * 3 - lineTime + (this.isLine1 ? 0 : Math.PI)) * 80 * env;
                
                let wiggle = Math.sin(this.phase + this.y * 0.05) * 5;
                let finalX = baseX + offset + this.driftX + wiggle;
                
                ctx.beginPath();
                ctx.arc(finalX, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = `rgba(150, 150, 150, ${this.opacity})`;
                ctx.fill();
            }
        }
        const bubbles = Array.from({length: 50}, () => new Bubble());

        let vibrationTime = 0;
        let twisterTime = 0;
        
        let beatProgress = 0;
        let isBeating = false;

        function scheduleNextBeat() {
            const nextInterval = Math.random() * 2000 + 1000;
            setTimeout(() => {
                isBeating = true;
                beatProgress = 0;
                scheduleNextBeat();
            }, nextInterval);
        }
        scheduleNextBeat();

        function drawTwistingLines() {
            twisterTime += 0.003;
            
            bgCtx.strokeStyle = 'rgba(150, 150, 150, 0.4)';
            bgCtx.lineWidth = 1.2;

            bgCtx.beginPath();
            for (let y = 0; y <= ch; y += 5) {
                let progress = y / ch;
                let baseX = progress * cw; 
                let env = Math.sin(progress * Math.PI);
                let offset = Math.sin(progress * Math.PI * 3 - twisterTime) * 80 * env;
                
                let x = baseX + offset;
                if (y === 0) bgCtx.moveTo(x, y);
                else bgCtx.lineTo(x, y);
            }
            bgCtx.stroke();

            bgCtx.beginPath();
            for (let y = 0; y <= ch; y += 5) {
                let progress = y / ch;
                let baseX = cw - progress * cw; 
                let env = Math.sin(progress * Math.PI);
                let offset = Math.sin(progress * Math.PI * 3 - twisterTime + Math.PI) * 80 * env;
                
                let x = baseX + offset;
                if (y === 0) bgCtx.moveTo(x, y);
                else bgCtx.lineTo(x, y);
            }
            bgCtx.stroke();
        }

        function drawDynamicSpectrum() {
            bgCtx.strokeStyle = 'rgba(0, 0, 0, 0.25)';
            bgCtx.lineWidth = 1;
            bgCtx.beginPath();
            
            const centerY = ch / 2;
            vibrationTime += 0.08;
            
            let currentBeat = 0;
            if (isBeating) {
                beatProgress += 0.06;
                if (beatProgress >= 1) {
                    beatProgress = 1;
                    isBeating = false;
                }
                currentBeat = Math.pow(Math.sin(beatProgress * Math.PI), 4);
            }
            
            for(let x = 0; x < cw; x += 2) {
                let cx = cw / 2;
                let dx = x - cx;
                
                let baseJitter = (Math.random() - 0.5) * 2;
                
                let ecg = 0;
                if (dx > -150 && dx < 150) {
                    if (dx > -100 && dx < -70) ecg = 12 * Math.sin(Math.PI * (dx + 100) / 30);
                    else if (dx >= -20 && dx < -10) ecg = -10 * (dx + 20)/10; 
                    else if (dx >= -10 && dx < 0) ecg = -10 + 130 * (dx + 10)/10; 
                    else if (dx >= 0 && dx < 10) ecg = 120 - 150 * (dx)/10; 
                    else if (dx >= 10 && dx < 25) ecg = -30 + 30 * (dx - 10)/15; 
                    else if (dx >= 50 && dx < 100) ecg = 25 * Math.sin(Math.PI * (dx - 50) / 50); 
                }
                
                let beatScale = 1 + currentBeat * 0.5;
                
                let spectrumEnv = Math.exp(-Math.pow(dx/150, 2));
                let spectrumVibe = Math.sin(x * 0.8 + vibrationTime * 20) * Math.cos(x * 0.3 - vibrationTime * 10) * 15 * spectrumEnv;
                let randomSpike = (Math.random() - 0.5) * 15 * spectrumEnv * currentBeat;

                let finalY = centerY - (ecg * beatScale) + baseJitter + spectrumVibe + randomSpike;
                
                if (x === 0) bgCtx.moveTo(x, finalY);
                else bgCtx.lineTo(x, finalY);
            }
            bgCtx.stroke();
        }

        function drawGrid() {
            bgCtx.strokeStyle = 'rgba(0, 0, 0, 0.035)';
            bgCtx.lineWidth = 1;
            bgCtx.beginPath();
            for(let x = 0; x <= cw; x += 30) {
                bgCtx.moveTo(x, 0); bgCtx.lineTo(x, ch);
            }
            for(let y = 0; y <= ch; y += 30) {
                bgCtx.moveTo(0, y); bgCtx.lineTo(cw, y);
            }
            bgCtx.stroke();
        }

        function renderBg() {
            bgCtx.fillStyle = '#ffffff';
            bgCtx.fillRect(0, 0, cw, ch);
            
            drawTwistingLines();
            bubbles.forEach(b => { 
                b.update(); 
                b.draw(bgCtx, twisterTime); 
            });

            drawDynamicSpectrum();
            
            dataBars.forEach(b => { b.update(); b.draw(bgCtx); });
            
            drawGrid();
            
            requestAnimationFrame(renderBg);
        }
        renderBg();
    })();

    document.addEventListener("DOMContentLoaded", () => {
      const bootScreen = document.getElementById('initial-boot-screen');
      const bootTextAnim = document.getElementById('boot-text-anim');
      const bootFill = document.getElementById('boot-fill');
      const bootPerc = document.getElementById('boot-perc');
      const bootStartBtn = document.getElementById('boot-start-btn');

      const bootLines = [
        "初始化神经接口...",
        "校准神经链接...",
        "构建防火墙...",
        "验证访问权限...",
        "正在同步数据...",
        "建立安全连接...",
        "准备用户界面..."
      ];

      const totalDuration = 3000;
      let startProgressTime = null;

      function updateBootProgress(timestamp) {
        if (!startProgressTime) startProgressTime = timestamp;
        const elapsed = timestamp - startProgressTime;
        let progress = Math.min(elapsed / totalDuration, 1);
        
        bootFill.style.width = (progress * 100) + '%';
        bootPerc.innerText = Math.floor(progress * 100) + '%';
        
        if (progress < 1) {
          window.requestAnimationFrame(updateBootProgress);
        }
      }
      window.requestAnimationFrame(updateBootProgress);

      async function typeLine(text) {
        bootTextAnim.className = 'boot-text typing';
        bootTextAnim.innerHTML = '';
        const baseCharTime = 120 / text.length; 
        for(let i = 0; i < text.length; i++) {
          bootTextAnim.innerHTML += text[i];
          let delay = baseCharTime;
          if (Math.random() > 0.8) delay += 35; 
          await new Promise(r => setTimeout(r, delay));
        }
      }

      async function teleportLine() {
        bootTextAnim.className = 'boot-text teleporting';
        await new Promise(r => setTimeout(r, 260)); 
      }

      async function runBootSequence() {
        for(let i = 0; i < bootLines.length; i++) {
          await typeLine(bootLines[i]); 
          await teleportLine();         
          await new Promise(r => setTimeout(r, 20)); 
        }
        
        bootTextAnim.className = 'boot-text final-state';
        bootTextAnim.innerHTML = '准备完成';
        
        bootStartBtn.classList.add('show');
      }

      setTimeout(runBootSequence, 100);

      bootStartBtn.addEventListener('click', () => {
        bootScreen.style.transition = 'opacity 0.6s ease';
        bootScreen.style.opacity = '0';
        setTimeout(() => {
          bootScreen.style.display = 'none';
          if (sentryEye.classList.contains('idle')) {
              startGlintScan();
          }
        }, 600);
      });
    });

    const navHome = document.getElementById('nav-home');
    
    const homeView = document.getElementById('home-view');
    const directoryView = document.getElementById('directory-view');
    
    const btnWiki = document.getElementById('nav-wiki-btn');
    const btnSheets = document.getElementById('nav-sheets-btn');
    const btnGroup = document.getElementById('nav-group-btn');
    const panelWiki = document.getElementById('panel-wiki');
    const panelSheets = document.getElementById('panel-sheets');
    const panelGroup = document.getElementById('panel-group');

    const sentryEye = document.getElementById('sys-indicator');
    const sentryGlint = sentryEye.querySelector('.sentry-glint');
    let glintScanInterval = null;

    function moveSentryGlint() {
        if (!sentryEye.classList.contains('idle')) return; 

        const minCoord = 18.5;
        const maxCoord = 21.5;

        const nextCx = (Math.random() * (maxCoord - minCoord) + minCoord).toFixed(1);
        const nextCy = (Math.random() * (maxCoord - minCoord) + minCoord).toFixed(1);

        sentryGlint.setAttribute('cx', nextCx);
        sentryGlint.setAttribute('cy', nextCy);
    }

    function startGlintScan() {
        if (glintScanInterval) {
            clearInterval(glintScanInterval);
        }
        const intervalDuration = Math.random() * (500 - 200) + 200;
        glintScanInterval = setInterval(moveSentryGlint, intervalDuration);
    }

    function stopGlintScan() {
        if (glintScanInterval) {
            clearInterval(glintScanInterval);
            glintScanInterval = null;
        }
        sentryGlint.setAttribute('cx', 20);
        sentryGlint.setAttribute('cy', 20);
    }


    function triggerSentryScan() {
      const indicator = document.getElementById('sys-indicator');
      if (indicator) {
        if (indicator.classList.contains('idle')) {
            stopGlintScan();
        }

        indicator.classList.remove('idle');
        indicator.classList.add('processing');

        setTimeout(() => {
          indicator.classList.remove('processing');
          indicator.classList.add('idle');
          startGlintScan();
        }, 1200);
      }
    }

    function closeAllPanels() {
      panelWiki.classList.remove('active');
      panelSheets.classList.remove('active');
      panelGroup.classList.remove('active');
    }

    btnWiki.addEventListener('click', function(e) {
      e.preventDefault();
      if (panelWiki.classList.contains('active')) {
        closeAllPanels(); 
      } else {
        closeAllPanels(); 
        panelWiki.classList.add('active');
      }
    });

    btnSheets.addEventListener('click', function(e) {
      e.preventDefault();
      if (panelSheets.classList.contains('active')) {
        closeAllPanels(); 
      } else {
        closeAllPanels(); 
        panelSheets.classList.add('active');
      }
    });

    btnGroup.addEventListener('click', function(e) {
      e.preventDefault();
      if (panelGroup.classList.contains('active')) {
        closeAllPanels();
      } else {
        closeAllPanels();
        panelGroup.classList.add('active');
      }
    });
    
    const loadingOverlay = document.getElementById('loading-overlay');
    const loadingFill = document.getElementById('loading-fill');
    const loadingText = document.getElementById('loading-text');

    function playTransitionAnimation(callback) {
      closeAllPanels(); 
      triggerSentryScan(); 

      loadingOverlay.style.display = 'flex';
      loadingFill.style.width = '0%';
      loadingText.innerText = '0%';

      let startTimestamp = null;
      const duration = 1200; 

      function step(timestamp) {
        if (!startTimestamp) startTimestamp = timestamp;
        const elapsed = timestamp - startTimestamp;
        
        let progress = Math.min(elapsed / duration, 1);
        
        loadingFill.style.width = (progress * 100) + '%';
        loadingText.innerText = Math.floor(progress * 100) + '%';

        if (progress < 1) {
          window.requestAnimationFrame(step);
        } else {
          if (callback) callback();
          loadingOverlay.style.display = 'none';
        }
      }

      window.requestAnimationFrame(step);
    }

    navHome.addEventListener('click', function(e) {
      e.preventDefault();
      closeAllPanels(); 
      if (homeView.style.display === 'block' || homeView.style.display === '') return;
      playTransitionAnimation(() => {
        directoryView.style.display = 'none'; 
        homeView.style.display = 'block';
      });
    });

    const otherTriggers = document.querySelectorAll('.nav-trigger');
    otherTriggers.forEach(trigger => {
      trigger.addEventListener('click', function(e) {
        e.preventDefault(); 
        
        let targetDir = this.getAttribute('data-dir');
        let titleText = this.getAttribute('data-title') || this.innerText;
        let syncTarget = this.getAttribute('data-sync-target'); 

        playTransitionAnimation(() => {
          if (targetDir) {
            homeView.style.display = 'none';
            directoryView.style.display = 'block';

            let dynTitle = document.getElementById('dir-dynamic-title');
            dynTitle.innerText = titleText;
            
            if(syncTarget) {
                dynTitle.setAttribute('data-sync-id', syncTarget);
            } else {
                dynTitle.removeAttribute('data-sync-id');
            }

            document.querySelectorAll('.dir-specific-content').forEach(el => {
              el.style.display = 'none';
            });

            let targetContent = document.getElementById('dir-content-' + targetDir);
            
            let commonHeader = document.getElementById('dir-common-header');
            
            if (targetContent) {
              targetContent.style.display = 'block';
              
              if (targetContent.classList.contains('dh-layout-wrapper')) {
                  if (commonHeader) commonHeader.style.display = 'none';
              } else {
                  if (commonHeader) commonHeader.style.display = 'block';
              }
            }
          } else {
            console.log("建设中：" + titleText);
          }
        });
      });
    });

    const expandableBoxes = document.querySelectorAll('.card-item, .about-text-box');
    expandableBoxes.forEach(box => {
      box.addEventListener('click', function() {
        this.classList.toggle('expanded');
      });
    });

    document.addEventListener('input', function(e) {
      if (e.target && e.target.hasAttribute('data-sync-id')) {
        let syncId = e.target.getAttribute('data-sync-id');
        let newVal = e.target.innerText;
        
        document.querySelectorAll(`[data-sync-id="${syncId}"]`).forEach(el => {
          if (el !== e.target && el.innerText !== newVal) {
            el.innerText = newVal;
          }
        });
        
        document.querySelectorAll(`a[data-sync-target="${syncId}"]`).forEach(btn => {
           btn.setAttribute('data-title', newVal);
        });
      }
    });

    document.addEventListener('keydown', function(e) {
      if (e.target && e.target.hasAttribute('contenteditable') && e.key === 'Enter') {
        if (!e.target.classList.contains('editable-content')) {
          e.preventDefault();
          e.target.blur(); 
        }
      }
    });

    (function initOscilloscope() {
        const oscBox = document.querySelector('.osc-bounding-box');
        const oscEl = document.querySelector('.oscilloscope');
        if(oscBox && oscEl) {
            oscBox.addEventListener('dblclick', () => {
                oscEl.classList.toggle('revealed');
            });
        }

        const canvas = document.getElementById('noiseCanvas');
        if(!canvas) return;
        const ctx = canvas.getContext('2d');
        canvas.width = 180; 
        canvas.height = 145;

        let animationFrameId;
        let isSnowing = true; 

        function drawNoise() {
            if (!isSnowing) return; 
            
            const imageData = ctx.createImageData(canvas.width, canvas.height);
            const data = imageData.data;
            
            for (let i = 0; i < data.length; i += 4) {
                const noise = Math.random() * 255;
                data[i] = 0;             
                data[i + 1] = noise;     
                data[i + 2] = 0;         
                data[i + 3] = 255;       
            }
            
            ctx.putImageData(imageData, 0, 0);
            animationFrameId = requestAnimationFrame(drawNoise);
        }

        drawNoise(); 

        const STEPS = 11; 
        const MIN_ANGLE = -150;
        const MAX_ANGLE = 150;
        const ANGLE_PER_STEP = (MAX_ANGLE - MIN_ANGLE) / (STEPS - 1);

        function generateScale(containerId) {
            const container = document.getElementById(containerId);
            if(!container) return;
            const centerX = 60; 
            const centerY = 60; 
            const radiusText = 55; 

            for (let i = 0; i < STEPS; i++) {
                const angleDeg = MIN_ANGLE + (i * ANGLE_PER_STEP);
                const angleRad = (angleDeg - 90) * (Math.PI / 180);
                
                const mark = document.createElement('div');
                mark.className = 'scale-mark';
                mark.style.left = '50%';
                mark.style.top = '50%';
                mark.style.transform = `translate(-50%, -50%) rotate(${angleDeg}deg) translateY(-42px)`;
                
                const text = document.createElement('div');
                text.className = 'scale-text';
                
                const tx = centerX + radiusText * Math.cos(angleRad);
                const ty = centerY + radiusText * Math.sin(angleRad);
                
                text.style.left = `${tx}px`;
                text.style.top = `${ty}px`;
                text.style.transform = `translate(-50%, -50%)`; 
                text.innerText = i; 
                
                container.appendChild(mark);
                container.appendChild(text);
            }
        }

        generateScale('scale1');
        generateScale('scale2');
        generateScale('scale3');

        let activeKnob = null;
        let activeKnobCenter = { x: 0, y: 0 };

        const knobs = [
            document.getElementById('knob1'),
            document.getElementById('knob2'),
            document.getElementById('knob3')
        ];
        
        const led = document.getElementById('status-led');

        function updateKnobTransform(knob, step) {
            const angle = MIN_ANGLE + (step * ANGLE_PER_STEP);
            knob.style.transform = `rotate(${angle}deg)`;
            knob.dataset.step = step;
        }

        function blinkLed() {
            if(!led) return;
            led.classList.add('blink');
            setTimeout(() => led.classList.remove('blink'), 150);
        }

        function startDrag(e, knob) {
            activeKnob = knob;
            const rect = knob.getBoundingClientRect();
            activeKnobCenter = {
                x: rect.left + rect.width / 2,
                y: rect.top + rect.height / 2
            };
            document.body.style.cursor = 'grabbing';
        }

        function moveDrag(clientX, clientY) {
            if (!activeKnob) return;
            
            const dx = clientX - activeKnobCenter.x;
            const dy = clientY - activeKnobCenter.y;
            
            let angleDeg = Math.atan2(dy, dx) * (180 / Math.PI) + 90;
            
            if (angleDeg > 180) angleDeg -= 360;
            if (angleDeg < -180) angleDeg += 360;
            
            let newStep = Math.round((angleDeg - MIN_ANGLE) / ANGLE_PER_STEP);
            
            newStep = Math.max(0, Math.min(STEPS - 1, newStep));
            
            if (newStep !== parseInt(activeKnob.dataset.step, 10)) {
                updateKnobTransform(activeKnob, newStep);
                blinkLed(); 
                checkEasterEgg(); 
            }
        }

        function endDrag() {
            activeKnob = null;
            document.body.style.cursor = 'default';
        }

        knobs.forEach(knob => {
            if(!knob) return;
            updateKnobTransform(knob, 0);

            knob.addEventListener('mousedown', (e) => {
                startDrag(e, knob);
            });

            knob.addEventListener('touchstart', (e) => {
                e.preventDefault();
                startDrag(e.touches[0], knob);
            }, { passive: false });
        });

        window.addEventListener('mousemove', (e) => {
            moveDrag(e.clientX, e.clientY);
        });
        window.addEventListener('mouseup', endDrag);

        window.addEventListener('touchmove', (e) => {
            if (!activeKnob) return;
            e.preventDefault();
            moveDrag(e.touches[0].clientX, e.touches[0].clientY);
        }, { passive: false });
        
        window.addEventListener('touchend', endDrag);
        window.addEventListener('touchcancel', endDrag);

        let audioCtx;
        let noiseSource;
        let noiseGain;
        let isNoiseOn = false;
        
        const btnNoise = document.getElementById('btn-noise');
        const cd1Audio = document.getElementById('cd1-audio');
        
        const SECRET_CODE = [4, 8, 9];
        let easterEggTriggered = false;

        if(btnNoise) {
            btnNoise.addEventListener('click', () => {
                if (!audioCtx) {
                    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                }
                
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume();
                }

                isNoiseOn = !isNoiseOn;
                
                if (isNoiseOn) {
                    btnNoise.classList.add('active');
                    if (!easterEggTriggered) {
                        startWhiteNoise();
                    }
                } else {
                    btnNoise.classList.remove('active');
                    stopWhiteNoise();
                }
            });
        }

        function startWhiteNoise() {
            if (!audioCtx) return;
            const bufferSize = audioCtx.sampleRate * 2; 
            const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
            const data = buffer.getChannelData(0);
            
            for (let i = 0; i < bufferSize; i++) {
                data[i] = Math.random() * 2 - 1; 
            }
            
            noiseSource = audioCtx.createBufferSource();
            noiseSource.buffer = buffer;
            noiseSource.loop = true;
            
            noiseGain = audioCtx.createGain();
            noiseGain.gain.value = 0.05; 
            
            noiseSource.connect(noiseGain);
            noiseGain.connect(audioCtx.destination);
            noiseSource.start();
        }

        function stopWhiteNoise() {
            if (noiseSource) {
                noiseSource.stop();
                noiseSource.disconnect();
                noiseSource = null;
            }
        }

        function checkEasterEgg() {
            if(!knobs[0] || !knobs[1] || !knobs[2]) return;
            const v1 = parseInt(knobs[0].dataset.step, 10);
            const v2 = parseInt(knobs[1].dataset.step, 10);
            const v3 = parseInt(knobs[2].dataset.step, 10);

            const isCodeCorrect = (v1 === SECRET_CODE[0] && v2 === SECRET_CODE[1] && v3 === SECRET_CODE[2]);

            if (isCodeCorrect && !easterEggTriggered) {
                triggerEasterEgg();
            } else if (!isCodeCorrect && easterEggTriggered) {
                resetEasterEgg();
            }
        }
        
        function resetEasterEgg() {
            easterEggTriggered = false;
            
            if(cd1Audio) {
                cd1Audio.pause();
                cd1Audio.currentTime = 0;
            }
            
            if(led) {
                led.style.backgroundColor = '';
                led.style.boxShadow = '';
            }
            
            if (!isSnowing) {
                isSnowing = true;
                drawNoise();
            }
            
            if (isNoiseOn) {
                startWhiteNoise();
            }
        }

        function triggerEasterEgg() {
            easterEggTriggered = true;
            
            stopWhiteNoise();
            isSnowing = false; 
            ctx.fillStyle = '#0f220f'; 
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            if(led) {
                led.style.backgroundColor = '#55ff55';
                led.style.boxShadow = '0 0 15px #55ff55';
            }

            if(cd1Audio) {
                cd1Audio.play().catch(e => {
                    console.warn("请确保CD1文件存在于同级目录中。");
                });
            }
        }
    })();

  </script>

</body>
</html>
