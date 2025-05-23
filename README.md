
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎉 Birthday Surprise 🎉</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@400;700&display=swap');

body {
    margin: 0;
    padding: 0;
    background-color: black; /* Start with black background */
    overflow-x: hidden;
    font-family: 'Poppins', sans-serif;
    text-align: center;
    color: white;
    transition: background 2s; /* Smooth background change */
}

#particles-js {
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: 0;
    top: 0;
    left: 0;
    display: none; /* Hidden initially */
}

#content {
    position: relative;
    z-index: 10;
    padding-top: 10%;
}

button {
    margin-top: 20px;
    padding: 20px 50px;
    font-size: 30px;
    border: none;
    border-radius: 50px;
    background: linear-gradient(45deg, #ff6ec4, #7873f5);
    color: white;
    cursor: pointer;
    box-shadow: 0 0 20px rgba(255,110,196,0.7);
    transition: 0.3s;
}

button:hover {
    transform: scale(1.1);
    box-shadow: 0 0 30px rgba(255,110,196,1);
}

#countdown {
    font-size: 100px;
    display: none;
    margin-top: 20px;
    animation: fadeIn 1s;
    font-family: 'Pacifico', cursive;
}

#happyBirthdayText {
    font-family: 'Pacifico', cursive;
    font-size: 80px;
    display: none;
    margin-top: 30px;
    animation: glow 1s infinite alternate;
}

@keyframes glow {
    from { text-shadow: 0 0 10px #ff6ec4, 0 0 20px #ff6ec4; }
    to { text-shadow: 0 0 20px #ff6ec4, 0 0 30px #ff6ec4; }
}

#cake {
    font-size: 150px;
    margin-top: 20px;
    display: none;
    animation: bounce 2s infinite;
}

@keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
}

#note {
    font-family: 'Pacifico', cursive;
    font-size: 30px;
    padding: 30px;
    margin: 100px auto;
    display: none;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    max-width: 1000px;
    animation: fadeSlideUp 2s;
}

@keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(50px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Balloons */
.balloon {
    width: 50px;
    height: 70px;
    background: radial-gradient(circle, pink, hotpink);
    border-radius: 50% 50% 45% 45%;
    position: absolute;
    bottom: -100px;
    animation: floatBalloon 10s infinite;
    z-index: 1;
}

@keyframes floatBalloon {
    0% { transform: translateY(0) rotate(0deg);}
    50% { transform: translateY(-500px) rotate(10deg);}
    100% { transform: translateY(-1000px) rotate(-10deg);}
}

</style>
</head>
<body>

<!-- Particle background -->
<div id="particles-js"></div>

<!-- Balloons (hidden initially) -->
<div id="balloons-container"></div>

<!-- Music -->
<audio id="birthdayMusic" loop autoplay muted>
  <source src="https://assets.mixkit.co/music/preview/mixkit-happy-birthday-to-you-956.mp3" type="audio/mp3">
</audio>

<div id="content">
    <button id="startButton" onclick="startSurprise()">Lights On ✨</button>
    <div id="countdown"></div>
    <div id="happyBirthdayText">🎉 Happiest Birthday! 🎉<br> 🎉My Dear Angry Bird🎉</div>
    <div id="cake">🎂</div>
    <button id="cakeButton" onclick="cutCake()" style="display:none;">Cut the Cake 🍰</button>
    <button id="giftButton" onclick="showNote()" style="display:none;">Open Your Gift 🎁</button>
    <div id="note"></div>
</div>

<!-- JS Scripts -->
<script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/party-js@latest/bundle/party.min.js"></script>

<script>
function startSurprise() {
    document.getElementById('startButton').style.display = 'none';
    document.getElementById('countdown').style.display = 'block';
    let counter = 3;
    const countdownEl = document.getElementById('countdown');

    const interval = setInterval(() => {
        countdownEl.innerHTML = counter;
        counter--;
        if (counter < 0) {
            clearInterval(interval);
            turnOnLights();
        }
    }, 1000);
}

function turnOnLights() {
    document.getElementById('countdown').style.display = 'none';
    document.getElementById('happyBirthdayText').style.display = 'block';
    document.getElementById('cakeButton').style.display = 'inline-block';

    // Change background
    document.body.style.background = "linear-gradient(45deg, #ffecd2, #fcb69f, #a18cd1, #fbc2eb)";
    document.body.style.backgroundSize = "400% 400%";
    document.body.style.animation = "backgroundShift 20s ease infinite";

    // Start particles
    document.getElementById('particles-js').style.display = 'block';
    startParticles();

    // Play music
    document.getElementById('birthdayMusic').muted = false;
    document.getElementById('birthdayMusic').play();

    // Start balloons
    startBalloons();
}

// Animate background shift
const styleSheet = document.createElement("style");
styleSheet.type = "text/css";
styleSheet.innerText = `
@keyframes backgroundShift {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
}
`;
document.head.appendChild(styleSheet);

function startParticles() {
    particlesJS("particles-js", {
        "particles": {
            "number": { "value": 80 },
            "color": { "value": "#ffffff" },
            "shape": { "type": "circle" },
            "opacity": { "value": 0.6, "random": true },
            "size": { "value": 4, "random": true },
            "move": { "enable": true, "speed": 2 }
        },
        "interactivity": {
            "events": { "onhover": { "enable": true, "mode": "repulse" } }
        },
        "retina_detect": true
    });
}

function startBalloons() {
    const container = document.getElementById('balloons-container');
    for (let i = 0; i < 20; i++) {
        let balloon = document.createElement('div');
        balloon.className = 'balloon';
        balloon.style.left = Math.random() * 100 + 'vw';
        balloon.style.animationDuration = (8 + Math.random() * 5) + 's';
        container.appendChild(balloon);
    }
}

function cutCake() {
    document.getElementById('cake').style.display = 'block';
    document.getElementById('cakeButton').style.display = 'none';
    document.getElementById('giftButton').style.display = 'inline-block';

    // Fireworks
    party.sparkles(document.getElementById('cake'), {
        count: 100,
        speed: 2,
        spread: 360
    });

    // Confetti
    confetti({
        particleCount: 200,
        spread: 70,
        origin: { y: 0.6 }
    });
}

function showNote() {
    document.getElementById('giftButton').style.display = 'none';
    document.getElementById('note').style.display = 'block';
    document.getElementById('note').innerHTML = `
        <h1>🌟 Happy Birthday Varun 🌟</h1>
        <p>
        To the most amazing person in my life, <br><br>
        Today is the day we celebrate YOU! 🎉 <br>
        You bring so much joy, love, and laughter to the world around you. It's incredible how you make everything better simply by being yourself. Your kindness, your heart, and your strength are qualities that I admire and cherish deeply. <br><br>

        Every day spent with you is a reminder of how lucky I am to have you by my side. Whether it’s sharing quiet moments or crazy adventures. You have this special way of making life brighter, and today, it’s time to shine even brighter than ever! ✨ <br><br>

        As you step into another year of your amazing life, know that the best is yet to come. May this year bring you endless happiness, growth, and success in everything you do. May your heart always be full of joy, and may you continue to be the incredible person you are. There’s no one quite like you, and I feel beyond lucky to celebrate this special day with you. 💖 <br><br>

        Remember, the journey ahead is full of endless possibilities, and I can’t wait to see all the beautiful things you will achieve. Keep dreaming big, reaching for the stars, and never stop being the wonderful, unique person you are. Happy Birthday again, my dear! 🥳 <br><br>

        Enjoy every moment of today, and know that no matter where life takes us, I’ll always be here, cheering you on, supporting you, and loving you every step of the way. 💫🎂

        Here's to many more birthdays, adventures, and precious memories together! 🎈
        </p>
 <h2 style="margin-top: 50px;">❤️ Yours Loving ❤️ <br> ❤️ Laadli ❤️ </h2>
        <img src="yours.loving.jpg" alt="Yours Loving" style="margin-top: 20px; max-width: 90%; border-radius: 20px; box-shadow: 0 0 20px rgba(0,0,0,0.5);" />	
    `;
    document.getElementById('note').scrollIntoView({ behavior: 'smooth' });
}
</script>

</body>
</html>
