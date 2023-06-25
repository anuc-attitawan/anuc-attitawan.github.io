<style>
    body {
        margin: 0;
        box-sizing: border-box;
        overflow: hidden;
    }

    #anuc {
        position: absolute;
        left: 0px;
        top: 0px;
        background-repeat: no-repeat;
        background-size: 75px;
        background-position: center;
        width: 100%;
        height: 100%;
        transition: width 0.5s, height 0.5s;
    }

    .anuc-activated {
        transition: all 0.3s ease-in-out;
        animation: wobbly-madness 3s infinite linear;
    }

    @keyframes wobbly-madness {
        0% {
            transform: scale(1) rotate(0deg);
            filter: hue-rotate(0deg);
        }
        50% {
            transform: scale(1.2) rotate(360deg);
            filter: hue-rotate(90deg);
        }
        100% {
            transform: scale(1) rotate(720deg);
            filter: hue-rotate(180deg);
        }
    }
</style>

<iframe id="anuc" width="100%" height="100%"
    src="https://www.youtube.com/embed/kpJOy-xdpHM?autoplay=1&controls=1&enablejsapi=1" frameborder="0"
    allowfullscreen></iframe>

<script>
    function ResizeAnuc() {
        var anucframe = document.getElementById('anuc');
        anucframe.style.width = '25%';
        anucframe.style.height = '25%';
        anucframe.classList.add('anuc-activated');
    }

    var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

    var player;
    function onYouTubePlayerAPIReady() {  
        player = new YT.Player('anuc', {
            height: '390',
            width: '640',      
            events: {
                'onStateChange': function(event) {
                    if (event.data == YT.PlayerState.PLAYING) {
                        console.log('Video is played!');
                        ResizeAnuc();
                        window.requestAnimationFrame(animate);
                    }
                }
            }  
        });           
    }

    let x = 0,
        y = 0,
        dirX = 1,
        dirY = 1;
    const speed = 2;
    let anuc = document.getElementById("anuc");
    const anucWidth = anuc.clientWidth;
    const anucHeight = anuc.clientHeight;

    function animate() {
        const screenHeight = document.body.clientHeight * 1.75;
        const screenWidth = document.body.clientWidth * 1.75;

        if (y + anucHeight >= screenHeight || y < 0) {
            dirY *= -1;
        }
        if (x + anucWidth >= screenWidth || x < 0) {
            dirX *= -1;
        }
        x += dirX * speed;
        y += dirY * speed;
        anuc.style.left = x + "px";
        anuc.style.top = y + "px";
        window.requestAnimationFrame(animate);
    }

    console.log("Welcome to the crazy rave party with Anuc Attitawan!");

    function raveParty() {
        setInterval(() => {
            const hue = Math.floor(Math.random() * 360);
            document.body.style.backgroundColor = `hsl(${hue}, 100%, 50%)`;
        }, 100);

        setInterval(() => {
            const randomRotation = Math.floor(Math.random() * 360);
            const randomScale = 1 + Math.random();
            const randomHueRotation = Math.floor(Math.random() * 360);
            anuc.style.transform = `rotate(${randomRotation}deg) scale(${randomScale})`;
            anuc.style.filter = `hue-rotate(${randomHueRotation}deg)`;
        }, 3000);
    }

    raveParty();
    document.addEventListener("DOMContentLoaded", function(event) {
      var item = document.getElementById("anuc");
        
      document.addEventListener("click", function(event) {
        var newItem = item.cloneNode(true);
        var xPos = Math.random() * (window.innerWidth - 50); // Adjust 50 to match the item's width
        var yPos = Math.random() * (window.innerHeight - 50); // Adjust 50 to match the item's height

        newItem.style.left = xPos + "px";
        newItem.style.top = yPos + "px";

        document.body.appendChild(newItem);
      });
    });
    
    // Additional effects
    
    function shakeElement(element) {
        const randomRotation = Math.floor(Math.random() * 20) - 10;
        const randomX = Math.floor(Math.random() * 10) - 5;
        const randomY = Math.floor(Math.random() * 10) - 5;
        element.style.transform = `rotate(${randomRotation}deg) translate(${randomX}px, ${randomY}px)`;
        setTimeout(() => {
            element.style.transform = "";
        }, 100);
    }
    
    setInterval(() => {
        shakeElement(anuc);
    }, 2000);
    
    function addRandomElements() {
        const elementCount = Math.floor(Math.random() * 10) + 5;
        
        for (let i = 0; i < elementCount; i++) {
            const newElement = document.createElement("div");
            newElement.classList.add("random-element");
            newElement.style.left = Math.random() * (window.innerWidth - 50) + "px";
            newElement.style.top = Math.random() * (window.innerHeight - 50) + "px";
            document.body.appendChild(newElement);
        }
    }
    
    setInterval(() => {
        addRandomElements();
    }, 5000);
</script>
