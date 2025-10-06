<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Man Page Animation</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.1/anime.min.js"></script>
  <style>
    body {
      margin: 0;
      padding: 20px;
      background: #0a0a0a;
      font-family: 'Courier New', monospace;
      color: #00ff00;
      min-height: 100vh;
    }
    
    .manpage {
      max-width: 800px;
      margin: 0 auto;
      background: #000;
      padding: 30px;
      border: 2px solid #00ff00;
      box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
    }
    
    .header {
      text-align: center;
      border-bottom: 1px solid #00ff00;
      padding-bottom: 10px;
      margin-bottom: 20px;
      opacity: 0;
    }
    
    .title {
      font-size: 24px;
      font-weight: bold;
      margin: 0;
    }
    
    .section {
      margin: 20px 0;
      opacity: 0;
    }
    
    .section-title {
      font-weight: bold;
      font-size: 18px;
      margin-bottom: 10px;
      color: #00ff00;
      text-transform: uppercase;
    }
    
    .content {
      margin-left: 20px;
      line-height: 1.6;
    }
    
    .command {
      color: #ffff00;
      font-weight: bold;
    }
    
    .option {
      color: #00ffff;
    }
    
    .cursor {
      display: inline-block;
      width: 10px;
      height: 18px;
      background: #00ff00;
      margin-left: 2px;
      animation: blink 1s infinite;
    }
    
    @keyframes blink {
      0%, 50% { opacity: 1; }
      51%, 100% { opacity: 0; }
    }
    
    .footer {
      text-align: center;
      margin-top: 30px;
      padding-top: 10px;
      border-top: 1px solid #00ff00;
      opacity: 0;
      font-size: 12px;
    }
    
    .glitch {
      position: relative;
    }
    
    .glitch::before,
    .glitch::after {
      content: attr(data-text);
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      opacity: 0;
    }
    
    .glitch::before {
      color: #ff00ff;
      animation: glitch-1 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite;
      clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
    }
    
    .glitch::after {
      color: #00ffff;
      animation: glitch-2 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite reverse;
      clip-path: polygon(0 60%, 100% 60%, 100% 100%, 0 100%);
    }
    
    @keyframes glitch-1 {
      0% { transform: translate(0); opacity: 0; }
      10% { transform: translate(-2px, -2px); opacity: 0.8; }
      20% { transform: translate(-3px, 0); opacity: 0; }
      30% { transform: translate(2px, -1px); opacity: 0.8; }
      40% { transform: translate(-1px, 2px); opacity: 0; }
      50% { transform: translate(-2px, -2px); opacity: 0.8; }
      60% { transform: translate(3px, 1px); opacity: 0; }
      100% { transform: translate(0); opacity: 0; }
    }
    
    @keyframes glitch-2 {
      0% { transform: translate(0); opacity: 0; }
      10% { transform: translate(2px, 2px); opacity: 0.8; }
      20% { transform: translate(3px, 0); opacity: 0; }
      30% { transform: translate(-2px, 1px); opacity: 0.8; }
      40% { transform: translate(1px, -2px); opacity: 0; }
      50% { transform: translate(2px, 2px); opacity: 0.8; }
      60% { transform: translate(-3px, -1px); opacity: 0; }
      100% { transform: translate(0); opacity: 0; }
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
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="300" height="300"><filter id="noise"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="4" /></filter><rect width="100%" height="100%" filter="url(%23noise)" /></svg>');
      animation: noise 0.2s steps(10) infinite;
    }
    
    @keyframes noise {
      0% { transform: translate(0, 0); }
      10% { transform: translate(-5%, -5%); }
      20% { transform: translate(-10%, 5%); }
      30% { transform: translate(5%, -10%); }
      40% { transform: translate(-5%, 15%); }
      50% { transform: translate(-10%, 5%); }
      60% { transform: translate(15%, 0); }
      70% { transform: translate(0, 10%); }
      80% { transform: translate(-15%, 0); }
      90% { transform: translate(10%, 5%); }
      100% { transform: translate(5%, 0); }
    }
  </style>
</head>
<body>
  <div class="scanline"></div>
  <div class="noise"></div>
  
  <div class="manpage">
    <div class="header">
      <h1 class="title glitch" data-text="AWESOME(1) User Commands AWESOME(1)">AWESOME(1) User Commands AWESOME(1)</h1>
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

  <script>
    // Animate header
    anime({
      targets: '.header',
      opacity: [0, 1],
      duration: 800,
      easing: 'easeInOutQuad'
    });

    // Animate sections sequentially
    anime({
      targets: '.section',
      opacity: [0, 1],
      translateY: [20, 0],
      delay: anime.stagger(300, {start: 800}),
      duration: 600,
      easing: 'easeOutQuad'
    });

    // Animate footer
    anime({
      targets: '.footer',
      opacity: [0, 1],
      duration: 600,
      delay: 3000,
      easing: 'easeInOutQuad'
    });

    // Random text scramble effect
    function scrambleText(element) {
      const originalText = element.textContent;
      const chars = '!@#$%^&*()_+-=[]{}|;:,.<>?/~`';
      let iterations = 0;
      const maxIterations = originalText.length;
      
      const interval = setInterval(() => {
        element.textContent = originalText.split('').map((char, index) => {
          if (index < iterations) {
            return originalText[index];
          }
          return chars[Math.floor(Math.random() * chars.length)];
        }).join('');
        
        if (iterations >= maxIterations) {
          clearInterval(interval);
          element.textContent = originalText;
        }
        iterations += 1/3;
      }, 30);
    }

    // Glitch random sections periodically
    setInterval(() => {
      const sections = document.querySelectorAll('.section-title');
      const randomSection = sections[Math.floor(Math.random() * sections.length)];
      scrambleText(randomSection);
    }, 5000);

    // Random color shift glitch
    setInterval(() => {
      const manpage = document.querySelector('.manpage');
      manpage.style.transform = `translate(${Math.random() * 4 - 2}px, ${Math.random() * 4 - 2}px)`;
      
      setTimeout(() => {
        manpage.style.transform = 'translate(0, 0)';
      }, 50);
    }, 3000);

    // Pulse border effect
    anime({
      targets: '.manpage',
      boxShadow: [
        '0 0 20px rgba(0, 255, 0, 0.3)',
        '0 0 40px rgba(0, 255, 0, 0.5)',
        '0 0 20px rgba(0, 255, 0, 0.3)'
      ],
      duration: 2000,
      loop: true,
      easing: 'easeInOutSine'
    });
    
    // Random flicker effect
    setInterval(() => {
      const content = document.querySelector('.content');
      anime({
        targets: content,
        opacity: [1, 0.7, 1, 0.8, 1],
        duration: 200,
        easing: 'linear'
      });
    }, 7000);
    
    // Horizontal line distortion
    setInterval(() => {
      const sections = document.querySelectorAll('.section');
      const randomSection = sections[Math.floor(Math.random() * sections.length)];
      
      anime({
        targets: randomSection,
        translateX: [0, -5, 5, -3, 3, 0],
        duration: 300,
        easing: 'easeInOutQuad'
      });
    }, 4000);
  </script>
</body>
</html>
