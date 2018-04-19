---
title: "Can <cite class='kw'>rchess</cite> package help in improving my chess play ? <i>part 1</i>"
hidden: false
categories: games
tags: chess computer R
author: neonira
---
### Experimenting <cite class='kw'>rchess</cite> package
I am fan of chess. As a player, I face some real issues with my play and wish to know if <cite class='kw'>rchess</cite> could help improve my chess play. <br/><br/>
I have at least 2 ideas to test with <cite class='kw'>rchess</cite>. First one, is assessing easyness of chess diagrams and chess movies production. The second one, is about creating new analysis diagrams based on chessboard influence. 
			
### <cite class='kw'>rchess</cite> package discovery
Let's keep it simple. You should browse <a href='http://jkunst.com/rchess/'>http://jkunst.com/rchess/</a> to get some knowledge about how to use <cite class='kw'>rchess</cite>. This site is simply good and reliable source of information about <cite class='kw'>rchess</cite>.

After some experiments, I found it reliable and apart some diagram and graphical presentation issues that do not fit my mood, information and API seems to be really easy. I decided to configure it a little bit to change chess theme and chess diagram rendering with <cite class='kw'>ggplot</cite> R package. <br/><br/>

```R
uparrow <- '▲'
downarrow <- '▼'

managePerspective <- function() {
    b <- 'black'
    z <- sapply(1:nchar(b), function(n) substr(b, 1, n))
    p <- if (tolower(perspective_s) %in% z) b else 'white'
}

perspective <- managePerspective()

getBoardFromFen <- function(fen_s, move) {

    k <- ggchessboard(fen = fen_s,
                 cellcols = c("#8ca2ad", "#dee3e6"),
                 perspective = perspective,
                 piecesize = 16)

    sp <- base::strsplit(fen_s, ' ', fixed = TRUE)[[1]][2]

    playside <- if (perspective == 'black') {
      if (sp == 'b') uparrow else downarrow
    } else {
      if (sp == 'b') downarrow else uparrow
    }

    k <- k +
        scale_x_discrete(label = letters[if (perspective == 'black') 8:1 else 1:8]) +
        xlab(move) + ylab(playside)

    k <- k +  theme(axis.ticks = element_blank(), axis.title.y = element_text(vjust = .95, angle = 0))
    k
}
```
#### original image 
<img src='/images/games/d/original.png' width='600' alt='original image' title='original image'/>

#### customized image
<img src='/images/games/d/starting-position.png' width='600'  alt='customized image' title='customized image'/>

					
So, from now, on each image, we have
* on the left, an indicator of the side to play
* at the bottom, right column names to ease game progress follow-up. This works whatever the side view considered
* customized light and dark squarred colors
* no more x and y labels displayed
* removed the ticks on X and Y also

### Next parts
We'll create images and make <cite class='kw'>ffmpeg</cite> movie of a chess game. This will be achieved on part 2.  
And then, we'll create some more sophisticated images, arrange them side by side with game moves and chessboard influence zones. After recording images, we'll create a movie of these result and try to proceed to a complete chess game analysis, from the chessboard influence zones diagrams. This will be achieved on part 3. 

##### Note
Images made using <cite class='kw'>ggplot</cite> R base package.  
Movie montage achieved by external shell script instrumenting <cite class='kw'>ffmpeg</cite> as it appeared to be much faster and reliable than thru <cite class='kw'>animation</cite> R package. 

