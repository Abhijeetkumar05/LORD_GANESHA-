<div class="ganesha">
    <img src="lord ganesha.jpg" width="600" />

    <div class="wrapper">
        <button data-type="laddu" class="glow-on-hover">Laddo</button>
        <button data-type="barfi" class="glow-on-hover">Barfi</button>
        <button data-type="fruit" class="glow-on-hover">Fruit</button>
        <button data-type="flower" class="glow-on-hover">Flower</button>
    </div>
    <span class="preloader"></span>
    <h2>Happy Ganesh Chaturthi..</h2>
</div>

<style>
    html {
        background-image: linear-gradient(144deg, #39afb5, #29bd2600);
        height: 100%;
    }

    body {
        color: rgba(255, 0, 0, 0.658);<
        display: -webkit-box;
        display: flex;
    }

    img {
        filter: drop-shadow(0px 0px 30px rgb(255, 0, 0));
        border-radius: 0%;
        height: 70%;
        width: auto;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center center;
    }

    /*
** Apply styles to the parent element
*/
    .ganesha {
        display: block;
        width: 100%;
        text-align: center;
    }

    h2 {
        position: absolute;
        left: 40%;
        font-size: 50px;
        /* color: white; */
        font-family: monospace;
        -webkit-text-stroke: 0vw #a89898;
    }

    h2::before {
        content: attr(data-text);
        position: absolute;
        top: 0;
        left: 0;
        width: 0%;
        height: 100%;
        color: #c5c5c5;
        -webkit-text-stroke: 0vw #d87272;
        border-right: 2px solid #ffffff;
        overflow: hidden;
        animation: slide 9s linear infinite;
        -webkit-animation: slide 9s linear infinite;
    }

    @keyframes slide {
        0% {
            width: 0;
        }

        70% {
            width: 105%;
        }
    }


    particle {
        position: fixed;
        top: 0;
        left: 0;
        opacity: 0;
        pointer-events: none;
        background-repeat: no-repeat;
        background-size: contain;
    }


    button {
        padding: 20px;
        margin: 10px;
        align-self: center;
    }

    .preloader {
        position: absolute;
        background: url(https://s3-us-west-2.amazonaws.com/s.cdpn.io/127738/fruit-face.png);
    }

    .glow-on-hover {
        width: 220px;
        height: 50px;
        border: none;
        outline: none;
        color: #fff;
        background: #111;
        cursor: pointer;
        position: relative;
        z-index: 0;
        border-radius: 10px;
    }

    .glow-on-hover:before {
        content: '';
        background: linear-gradient(45deg, #ff0000, #ff7300, #fffb00, #48ff00, #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
        position: absolute;
        top: -2px;
        left: -2px;
        background-size: 400%;
        z-index: -1;
        filter: blur(5px);
        width: calc(100% + 4px);
        height: calc(100% + 4px);
        animation: glowing 20s linear infinite;
        opacity: 0;
        transition: opacity .3s ease-in-out;
        border-radius: 10px;
    }

    .glow-on-hover:active {
        color: #000
    }

    .glow-on-hover:active:after {
        background: transparent;
    }

    .glow-on-hover:hover:before {
        opacity: 1;
    }

    .glow-on-hover:after {
        z-index: -1;
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        background: #111;
        left: 0;
        top: 0;
        border-radius: 10px;
    }

    @keyframes glowing {
        0% {
            background-position: 0 0;
        }

        50% {
            background-position: 400% 0;
        }

        100% {
            background-position: 0 0;
        }
    }
</style>

<script>

    function pop(e) {
        let amount = 30;
        switch (e.target.dataset.type) {
            case 'flower':
            case 'line':
                amount = 60;
                break;
        }
        // Quick check if user clicked the button using a keyboard
        if (e.clientX === 0 && e.clientY === 0) {
            const bbox = e.target.getBoundingClientRect();
            const x = bbox.left + bbox.width / 2;
            const y = bbox.top + bbox.height / 2;
            for (let i = 0; i < 30; i++) {
                // We call the function createParticle 30 times
                // We pass the coordinates of the button for x & y values
                createParticle(x, y, e.target.dataset.type);
            }
        } else {
            for (let i = 0; i < amount; i++) {
                createParticle(e.clientX, e.clientY + window.scrollY, e.target.dataset.type);
            }
        }
    }
    function createParticle(x, y, type) {
        const particle = document.createElement('particle');
        document.body.appendChild(particle);
        let width = Math.floor(Math.random() * 30 + 8);
        let height = width;
        let destinationX = (Math.random() - 0.5) * 300;
        let destinationY = (Math.random() - 0.5) * 300;
        let rotation = Math.random() * 520;
        let delay = Math.random() * 200;

        switch (type) {
            case 'laddu':
                particle.style.backgroundImage = 'url(laddu.png)';
                break;
            case 'barfi':
                particle.style.backgroundImage = 'url(barfi.png)';
                break;
            case 'fruit':
                particle.style.backgroundImage = 'url(fruit.png)';
                break;
            case 'flower':
                particle.style.backgroundImage = 'url(flower.png)';
                break;
            case 'line':
                var color = `hsl(${Math.random() * 90 + 90}, 70%, 50%)`;
                particle.style.background = 'black';
                height = 1;
                rotation += 1000;
                delay = Math.random() * 1000;
                break;
        }

        particle.style.width = `${width}px`;
        particle.style.height = `${height}px`;
        const animation = particle.animate([
            {
                transform: `translate(-50%, -50%) translate(${x}px, ${y}px) rotate(0deg)`,
                opacity: 1
            },
            {
                transform: `translate(-50%, -50%) translate(${x + destinationX}px, ${y + destinationY}px) rotate(${rotation}deg)`,
                opacity: 0
            }
        ], {
            duration: Math.random() * 1000 + 5000,
            easing: 'cubic-bezier(0, .9, .57, 1)',
            delay: delay
        });
        animation.onfinish = removeParticle;
    }
    function removeParticle(e) {
        e.srcElement.effect.target.remove();
    }

    if (document.body.animate) {
        document.querySelectorAll('button').forEach(button => button.addEventListener('click', pop));
    }

</script>
