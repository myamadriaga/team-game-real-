---
layout: default
title: Team Game
---


## Escape the Jungle! 

<span style="font-family: teko;">Abby M., Manahil K., Mya M., Sahana P.</span>

## About the game
Blogging in GitHub pages is a way to learn and code at the same time. 

- Plans, Lists, [Scrum Boards](https://clickup.com/blog/scrum-board/) help you to track key events, show progress and record time.  Effort is a big part of your class grade.  Show plans and time spent!
- [Hacks(Todo)](https://levelup.gitconnected.com/six-ultimate-daily-hacks-for-every-programmer-60f5f10feae) enable you to stay in focus with key requirements of the class.  Each Hack will produce Tangibles.
- Tangibles or [Tangible Artifacts](https://en.wikipedia.org/wiki/Artifact_(software_development)) are things you accumulate as a learner and coder. 

<head>
  <font face="Playfair Display"><title>snake High Score</title></font>
</head>
<body>
  <!-- Your game canvas or container -->
  
  <div>
    <font face="Playfair Display"><p class="fs-4">High score: <span id="highScore">0</span></p></font>
  </div>
 <script>
    (function(){
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