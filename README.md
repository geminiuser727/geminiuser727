<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Man Page Animation</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      background: #0a0a0a;
      font-family: 'Courier New', monospace;
      color: #00ff00;
      padding: 20px;
      min-height: 100vh;
      overflow-x: hidden;
    }
    
    .scanline {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(
        to bottom,
        transparent 50%,
        rgba(0, 255, 0, 0.05) 50%
      );
      background-size: 100% 4px;
      pointer-events: none;
      animation: scanline 8s linear infinite;
      z-index: 10;
    }
    
    @keyframes scanline {
      0% { transform: translateY(-100%); }
      100% { transform: translateY(100%); }
    }
    
    .noise {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      opacity: 0.03;
      z-index: 5;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="300" height="300"><filter id="n"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="4" /></filter><rect width="100%" height="100%" filter="url(%23n)" /></svg>');
      animation: noise 0.2s steps(10) infinite;
    }
    
    @keyframes noise {
      0%, 100% { transform: translate(0, 0); }
      10% { transform: translate(-5%, -5%); }
      20% { transform: translate(-10%, 5%); }
      30% { transform: translate(5%, -10%); }
      40% { transform: translate(-5%, 15%); }
      50% { transform: translate(-10%, 5%); }
      60% { transform: translate(15%, 0); }
      70% { transform: translate(0, 10%); }
      80% { transform: translate(-15%, 0); }
      90% { transform: translate(10%, 5%); }
    }
    
    .manpage {
      max-width: 800px;
      margin: 0 auto;
      background: #000;
      padding: 30px;
      border: 2px solid #00ff00;
      box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
      animation: 
        fadeIn 0.8s ease-out,
        pulse 2s ease-in-out infinite,
        jitter 3s ease-in-out infinite;
      position: relative;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    @keyframes pulse {
      0%, 100% { box-shadow: 0 0 20px rgba(0, 255, 0, 0.3); }
      50% { box-shadow: 0 0 40px rgba(0, 255, 0, 0.5); }
    }
    
    @keyframes jitter {
      0%, 100% { transform: translate(0, 0); }
      10% { transform: translate(-1px, 1px); }
      20% { transform: translate(1px, -1px); }
      30% { transform: translate(-1px, -1px); }
      40% { transform: translate(1px, 1px); }
      50% { transform: translate(-2px, 0); }
      60% { transform: translate(2px, 0); }
      70% { transform: translate(0, -1px); }
      80% { transform: translate(0, 1px); }
      90% { transform: translate(-1px, 0); }
    }
    
    .header {
      text-align: center;
      border-bottom: 1px solid #00ff00;
      padding-bottom: 10px;
      margin-bottom: 20px;
      animation: fadeIn 0.8s ease-out;
    }
    
    .title {
      font-size: 24px;
      font-weight: bold;
      position: relative;
      display: inline-block;
      animation: flicker 5s ease-in-out infinite;
    }
    
    .title::before,
    .title::after {
      content: attr(data-text);
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }
    
    .title::before {
      color: #ff00ff;
      animation: glitch-1 2.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite;
      clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
    }
    
    .title::after {
      color: #00ffff;
      animation: glitch-2 2.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite reverse;
      clip-path: polygon(0 60%, 100% 60%, 100% 100%, 0 100%);
    }
    
    @keyframes glitch-1 {
      0%, 95%, 100% { transform: translate(0); opacity: 0; }
      96% { transform: translate(-2px, -2px); opacity: 0.8; }
      97% { transform: translate(2px, 1px); opacity: 0.8; }
      98% { transform: translate(-1px, 2px); opacity: 0.8; }
      99% { transform: translate(1px, -1px); opacity: 0.8; }
    }
    
    @keyframes glitch-2 {
      0%, 95%, 100% { transform: translate(0); opacity: 0; }
      96% { transform: translate(2px, 2px); opacity: 0.8; }
      97% { transform: translate(-2px, -1px); opacity: 0.8; }
      98% { transform: translate(1px, -2px); opacity: 0.8; }
      99% { transform: translate(-1px, 1px); opacity: 0.8; }
    }
    
    @keyframes flicker {
      0%, 100% { opacity: 1; }
      41%, 43% { opacity: 0.8; }
      42% { opacity: 0.5; }
      44% { opacity: 1; }
      45% { opacity: 0.7; }
      46% { opacity: 1; }
    }
    
    .section {
      margin: 20px 0;
      animation: slideIn 0.6s ease-out backwards;
    }
    
    .section:nth-child(1) { animation-delay: 0.8s; }
    .section:nth-child(2) { animation-delay: 1.1s; }
    .section:nth-child(3) { animation-delay: 1.4s; }
    .section:nth-child(4) { animation-delay: 1.7s; }
    .section:nth-child(5) { animation-delay: 2s; }
    .section:nth-child(6) { animation-delay: 2.3s; }
    
    @keyframes slideIn {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    .section-title {
      font-weight: bold;
      font-size: 18px;
      margin-bottom: 10px;
      color: #00ff00;
      text-transform: uppercase;
      animation: textGlitch 7s ease-in-out infinite;
    }
    
    @keyframes textGlitch {
      0%, 90%, 100% { transform: translateX(0); }
      91% { transform: translateX(-3px); }
      92% { transform: translateX(3px); }
      93% { transform: translateX(-2px); }
      94% { transform: translateX(2px); }
      95% { transform: translateX(0); }
    }
    
    .content {
      margin-left: 20px;
      line-height: 1.6;
      animation: contentFlicker 10s ease-in-out infinite;
    }
    
    @keyframes contentFlicker {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.95; }
      50.5% { opacity: 0.85; }
      51% { opacity: 1; }
    }
    
    .command {
      color: #ffff00;
      font-weight: bold;
      text-shadow: 0 0 5px rgba(255, 255, 0, 0.5);
    }
    
    .option {
      color: #00ffff;
      text-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
    }
    
    .footer {
      text-align: center;
      margin-top: 30px;
      padding-top: 10px;
      border-top: 1px solid #00ff00;
      font-size: 12px;
      animation: fadeIn 0.6s ease-out 2.6s backwards;
    }
    
    @keyframes distort {
      0%, 100% { transform: translateX(0); }
      20% { transform: translateX(-2px); }
      40% { transform: translateX(2px); }
      60% { transform: translateX(-1px); }
      80% { transform: translateX(1px); }
    }
  </style>
</head>
<body>
  <div class="scanline"></div>
  <div class="noise"></div>
  
  <div class="manpage">
    <div class="header">
      <h1 class="title" data-text="AWESOME(1) User Commands AWESOME(1)">AWESOME(1) User Commands AWESOME(1)</h1>
    </div>
    
    <div class="section" id="name">
      <div class="section-title">Name</div>
      <div class="content">
        <span class="command">awesome</span> - make everything awesome
      </div>
    </div>
    
    <div class="section" id="synopsis">
      <div class="section-title">Synopsis</div>
      <div class="content">
        <span class="command">awesome</span> [<span class="option">-h</span>] [<span class="option">-v</span>] [<span class="option">--make-it-work</span>] [FILE...]
      </div>
    </div>
    
    <div class="section" id="description">
      <div class="section-title">Description</div>
      <div class="content">
        The <span class="command">awesome</span> command transforms ordinary operations into extraordinary experiences. It accepts input files and applies advanced awesomeness algorithms to produce optimal results.
      </div>
    </div>
    
    <div class="section" id="options">
      <div class="section-title">Options</div>
      <div class="content">
        <div style="margin-bottom: 10px;">
          <span class="option">-h, --help</span><br>
          &nbsp;&nbsp;&nbsp;&nbsp;Display this help message and exit
        </div>
        <div style="margin-bottom: 10px;">
          <span class="option">-v, --verbose</span><br>
          &nbsp;&nbsp;&nbsp;&nbsp;Enable verbose output mode
        </div>
        <div style="margin-bottom: 10px;">
          <span class="option">--make-it-work</span><br>
          &nbsp;&nbsp;&nbsp;&nbsp;Apply maximum awesomeness level
        </div>
      </div>
    </div>
    
    <div class="section" id="examples">
      <div class="section-title">Examples</div>
      <div class="content">
        $ <span class="command">awesome</span> <span class="option">--make-it-work</span> myfile.txt<br>
        $ <span class="command">awesome</span> <span class="option">-v</span> *.md
      </div>
    </div>
    
    <div class="footer">
      Version 1.0.0 - October 2025
    </div>
  </div>
</body>
</html>
