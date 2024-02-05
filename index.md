---
layout: default
title: Team Game
---
        
## <span style="font-family:Courier New; font-size: 30px;">Escape the Jungle!</span>

<span style="font-family:Courier New; font-size: 20px;">Abby M., Manahil K., Mya M., Sahana P.</span>

## <span style="font-family:Courier New; font-size: 24px;">About the game</span>



<head>
  <span style="font-family:Courier New; font-size: 20px;">snake High Score</span>

</head>
<body>
  <!-- Your game canvas or container -->
  
  <div>
    <font face="Courier New"><p class="fs-4">High score: <span id="highScore">0</span></p></font>
  </div>
 <script>
    {function(){
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        // HTML Game IDs
        const high_score = document.getElementById("highScore"); 
        // HTML Screen IDs (div)
        const SCREEN_MENU = -1, SCREEN_GAME_OVER=1, SCREEN_SETTING=2;
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");
        // HTML Event IDs (a tags)
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");
        /* Display Control */
        /////////////////////////////////////////////////////////////
        // 0 for the game
        // 1 for the main menu
        // 2 for the settings screen
        // 3 for the game over screen
            }
        }
        
