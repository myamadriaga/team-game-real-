---
layout: post
title:  Test Game
description: game
type: tangibles
courses: { compsci: {week: 2} }
---
<style>
    #canvas {
        margin: 0;
        border: 1px solid white;
    }
</style>
<canvas id='canvas'></canvas>
<script>
    let canvas = document.getElementById('canvas');
    let c = canvas.getContext('2d');
    canvas.width = 650;
    canvas.height = 400;
    let gravity = 1.5;
    class Platform {
        constructor(image) {
            this.position = {
                x: 0,
                y: 300
            }
            this.image = image;
            this.width = 650;
            this.height = 100;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
        }
    }
    class Tube {
        constructor(image) {
            this.position = {
                x: 500,
                y: 180
            }
            this.image = image;
            this.width = 100;
            this.height = 120;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
        }
    }
    class BlockObject {
        constructor(image) {
            this.position = {
                x: 200,
                y: 100
            };
            this.image = image;
            this.width = 158;
            this.height = 79;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y);
        }
    }
    //--
    // NEW CODE - CREATE GOOMBA CLASS
    //--
    class Goomba {
        constructor(image) {
            this.position = {
                x: 250,
                y: 245
            };
            this.image = image;
            this.width = 55;
            this.height = 55;
            this.velocity = {
                x: -2,
                y: 0
            }
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
        }
        update() {
            this.position.x += this.velocity.x;
            this.draw();
        }
    }
    let image = new Image()
    let imageTube = new Image()
    let imageBlock = new Image()
    image.src = 'https://samayass.github.io/samayaCSA/images/platform.png'
    imageTube.src = 'https://samayass.github.io/samayaCSA/images/tube.png'
    imageBlock.src = 'https://samayass.github.io/samayaCSA/images/box.png';
    //--
    // NEW CODE - ADD GOOMBA IMAGE
    //--
    let imageGoomba = new Image()
    imageGoomba.src = '{{site.baseurl}}/images/cute-pink-bow-png-0-removebg-preview.png';
    let platform = new Platform(image)
    let tube = new Tube(imageTube)
    let blockObject = new BlockObject(imageBlock)
    let goomba = new Goomba(imageGoomba)
    player = new Player()
    let keys = {
        right: {
            pressed: false
        },
        left: {
            pressed: false
        }
    }
    function animate() {
        requestAnimationFrame(animate);
        c.clearRect(0, 0, canvas.width, canvas.height);
        platform.draw();
        player.update();
        tube.draw();
        blockObject.draw();
        //--
        // NEW CODE - UPDATE GOOMBA ANIMATION
        //--
        goomba.update();
        if (
            player.position.y + player.height <= blockObject.position.y &&
            player.position.y + player.height + player.velocity.y >= blockObject.position.y &&
            player.position.x + player.width >= blockObject.position.x &&
            player.position.x <= blockObject.position.x + blockObject.width
        )
        {
            player.velocity.y = 0;
        }
        if (keys.right.pressed && player.position.x + player.width <= canvas.width - 50) {
            player.velocity.x = 15;
        } else if (keys.left.pressed && player.position.x >= 50) {
            player.velocity.x = -15;
        } else {
            player.velocity.x = 0;
        }
        if (
                player.position.y + player.height <= platform.position.y &&
                player.position.y + player.height + player.velocity.y >= platform.position.y &&
                player.position.x + player.width >= platform.position.x &&
                player.position.x <= platform.position.x + platform.width
            )
            {
                player.velocity.y = 0;
            }
        if (
                player.position.y + player.height <= tube.position.y &&
                player.position.y + player.height + player.velocity.y >= tube.position.y &&
                player.position.x + player.width >= tube.position.x &&
                player.position.x <= tube.position.x + tube.width
            ) {
                player.velocity.y = 0;
                player.position.y += 0.1
                player.velocity.y = 0.0001
                gravity = 0.2
            }
            if (player.position.y + player.height == tube.position.y + tube.height ||
                    player.position.y + player.height <= tube.position.y ||
                    player.position.x + player.width <= tube.position.x ||
                    player.position.x >= tube.position.x + tube.width) {
                        gravity = 1.5
                    }
        if (
                player.position.x + player.width<= tube.position.x &&
                player.position.x + player.width + player.velocity.x >= tube.position.x &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x >= tube.position.x + tube.width &&
                player.position.x + player.velocity.x <= tube.position.x + tube.width &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x >= tube.position.x &&
                player.position.x + player.velocity.x <= tube.position.x &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x + player.width <= tube.position.x + tube.width &&
                player.position.x + player.width + player.velocity.x >= tube.position.x + tube.width &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
            //--
            // NEW CODE - GOOMBA COLLISION DETECTION
            //--
        if(
            player.position.y + player.height <= goomba.position.y &&
            player.position.y + player.height + player.velocity.y >= goomba.position.y &&
            player.position.x + player.width >= goomba.position.x &&
            player.position.x <= goomba.position.x + goomba.width
        )
        {
            player.velocity.y = -20;
        }
        if (
            goomba.position.x >= platform.position.x &&
            goomba.position.x <= platform.position.x
        )
        {
            goomba.velocity.x = 2;
        }
        if (
            goomba.position.x + goomba.width <= tube.position.x &&
            goomba.position.x + goomba.width + goomba.velocity.x >= tube.position.x
        )
        {
            goomba.velocity.x = -2;
        }
    }
    animate();
    addEventListener('keydown', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = true;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = true;
                break;
            case 87:
                console.log('up');
                player.velocity.y -= 20;
                break;
        }
    });
    addEventListener('keyup', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = false;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = false;
                break;
            case 87:
                console.log('up');
                player.velocity.y = -20;
                break;
        }
    })
    //adding a character sprite sheet
        update() 
            this.draw();
            this.position.y += this.velocity.y;
            this.position.x += this.velocity.x;
            if (this.position.y + this.height + this.velocity.y <= canvas.height)
                this.velocity.y += gravity;
            else
                this.velocity.y = 0;
    // Create a player object
    player = new Player();
    //ADDING A CHARACTER SPRITE
            <img id="zoroSprite" src="{{site.baseurl}}/images/hello_kitty-removebg-preview.png">  // change sprite here
            
<script>
    // start on page load
    window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        const SPRITE_WIDTH = 39;  // matches sprite pixel width
        const SPRITE_HEIGHT = 45; // matches sprite pixel height
        const FRAME_LIMIT = 6;  // matches number of frames per sprite row, this code assume each row is same

        const SCALE_FACTOR = 3;  // control size of sprite on canvas
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;

        class zoro {
            constructor() {
                this.image = document.getElementById("zoroSprite");
                this.x = 0;
                this.y = 0;
                this.minFrame = 0;
                this.maxFrame = FRAME_LIMIT;
                this.frameX = 0;
                this.frameY = 0;
            }
            // draw dog object
            draw(context) {
                context.drawImage(
                    this.image,
                    this.frameX * SPRITE_WIDTH,
                    this.frameY * SPRITE_HEIGHT,
                    SPRITE_WIDTH,
                    SPRITE_HEIGHT,
                    this.x,
                    this.y,
                    canvas.width,
                    canvas.height
                );
            }

            // update frameX of object
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }

        // dog object
        const character = new zoro();
const controls = document.getElementById('controls');
controls.addEventListener('click', function (event) {
    if (event.target.tagName === 'INPUT') {
        const selectedAnimation = event.target.id;
        switch (selectedAnimation) {
            case 'idle':
                zoro.frameY = 0;
                break;
            case 'run':
                zoro.frameY = 1;
                break;
            case 'jump':
                zoro.frameY = 2;
                break;
            default:
                break;
        }

        // Increment the frameY property to make the position on the sprite sheet go lower
        zoro.frameY++;

        // You may want to reset frameY to 0 if it goes beyond a certain limit
        // For example, if you have only a few rows in your sprite sheet
        if (zoro.frameY >= 3) {
            zoro.frameY = 3;
        }
    }
});
        // update 
        // of dog object, action from idle, bark, walk radio control
       // const controls = document.getElementById('controls');
      //  controls.addEventListener('click', function (event) {
        //    console.log(event)
         //   if (event.target.tagName === 'INPUT') {
           //     const selectedAnimation = event.target.id;
            //    switch (selectedAnimation) {
               //     case 'idle':
                  //      zoro.frameY = 0;
                   //     break;
                 //   case 'run':
                 //       zoro.frameY = 1;
                 //       break;
                //    case 'jump':
                 //       zoro.frameY = 2;
                 //       break;
                 //   default:
                 //       break;
                     
         //       }
        //    }
      //  });

        // Animation recursive control function
        function animate() {
            // Clears the canvas to remove the previous frame.
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draws the current frame of the sprite.
            character.draw(ctx);

            // Updates the `frameX` property to prepare for the next frame in the sprite sheet.
            character.update();

            // Uses `requestAnimationFrame` to synchronize the animation loop with the display's refresh rate,
            // ensuring smooth visuals.
           // requestAnimationFrame(animate);
         setTimeout(function() {
    requestAnimationFrame(animate);
  }, 200);
        }
        // run 1st animate
        animate();
    });
  //  END OF CHARACTER ANIMATION
    });
    // Define keyboard keys and their states
    let keys = {
        right: {
            pressed: false
        },
        left: {
            pressed: false
        }
    };
    // Animation function to continuously update and render the canvas
    function animate() {
        requestAnimationFrame(animate);
        c.clearRect(0, 0, canvas.width, canvas.height);
        player.update();
        if (keys.right.pressed && player.position.x + player.width <= canvas.width - 50) {
            player.velocity.x = 15;
        } else if (keys.left.pressed && player.position.x >= 50) {
            player.velocity.x = -15;
        } else {
            player.velocity.x = 0;
        }
    }
    animate();
    // Event listener for keydown events
    addEventListener('keydown', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = true;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = true;
                break;
            case 87:
                console.log('up');
                player.velocity.y -= 20;
                break;
        }
    });
    // Event listener for keyup events
    addEventListener('keyup', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = false;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = false;
                break;
            case 87:
                console.log('up');
                player.velocity.y = -20;
                break;
        }
    });
</script>
</script>
    
