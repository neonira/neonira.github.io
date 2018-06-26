---
title: "Improving your chess play - part 4"
hidden: false
categories: games EN
tags: chess computer R
author: neonira
permalink: icp4
---
### Experimenting chessboard influence
This is the last post of a 4 posts serie, dedicated to chessplay and more specifically to the battle of influence on the chessboard.  
We are now trying to create a methodical appraoch to improve our chess play.  

In cas you missed previous posts, you may read <a href='/icp1'> part 1</a>, <a href='/icp2'> part 2</a>, and <a href='/icp3'> part 3</a>.
			
### Trials and errors 
Running the software on several games, it appears, that it was uneasy to have to check at both the chessboard position and the influence chessboard. So, to ease handling, we just came up with a split screen with on the left the chessboard position and on the right, the influence chessboard. This allows your eye to catch much more easily what's going on. Here is a sample 
<img src='/images/games/d/png-008.png' width='600' alt='split screen' title='split screen'/>
<br/>

### Static analysis
Looking at previous picture, you may know or discover, with a little experience, following facts 
* what pieces (yours or opponents) are takeable and you will also be knowledged about the number of exchanges you could do on that squarre to earn a piece
* what are the currently weak squarres on your defence and in your opponent defence
* what are the squarre that seem to be undisputed

These information are just factor to forge your decision. They have to be taken with consideration of the dynamic of the game, of the tactical opportunities, and also, of your ability and preference to play simplified or complexed games. 

### Going deeper 
If we consider previous picture, then we could proceed to a video montage of a whole chess game, and we could see how influence evolves through the entire game.
Here is an example, of the game played during [TCEC Season 11 - Superfinal](http://tcec.chessdom.com), between <cite class='kw'>Stockfish 260318</cite>, playing white side, and <cite class='kw'>Houdini 6.03</cite> playing black side. 

<video height="400" controls>
  <source src="/images/games/d/a-split.mp4" type="video/mp4">
 Your browser does not support the video tag.
</video> 
<br/>

Note, how the influence battle over the board evolves, and how <cite class='kw'>Stockfish 260318</cite> handles the game without any timeout. Quite impressive! 
You may compare this movie to the simpler one, just showing the game without the influence zone analysis. Which one do you prefer?

<video height="400" controls>
  <source src="/images/games/d/a.mp4" type="video/mp4">
 Your browser does not support the video tag.
</video> 


### Influence temporal diagram
Let's create the diagram of influence, for the whole game and see if we could learn something from it. We will compute the number of squarres, as already stated, but using half-move number as the index of a temporal analysis. thus we'll end up with a temporal diagram that could bring some light about the played game. Here's the result of a suche analysis, still for this game between those 2 software programs.
<img src='/images/games/d/sht.png' width='800' alt='split screen' title='split screen'/>
<br/>

Analyzing such diagram, can be helpful. In particular, here in this game between two super-human chess-playing software, it is quite clear that from half-move 70, <cite class='kw'>Stockfish</cite> has a surge in influence domination, while its opponent is simply collapsing on the number of controlled squarres.

### Conclusion
Influence analysis can help improve your chess play, and understand better what's going on on current position. It can also help in understanding more deeply some super software games. Hope you enjoyed this serie of 4 posts. Your comments and feedbacks are welcome. Let me know your opinion about this approach. Is it worth or not, having such analysis tool?


##### Note
Images made using <cite class='kw'>ggplot</cite> R base package.  
Movie montage achieved by external shell script instrumenting <cite class='kw'>ffmpeg</cite>. 



