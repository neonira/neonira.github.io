---
title: "Improving your chess play - part 2"
hidden: false
categories: games
tags: chess computer R
author: neonira
permalink: icp2
---
### Experimenting <cite class='kw'>rchess</cite> package
This is the second post of a serie, dedicated to <cite class='kw'>rchess</cite> R package.  
This week we aim to produce chess game half-move images and to proceed to a movie montage in order to get a video representative of the full chess game. 
In cas you missed first part, you may <a href='/icp1'> read part 1 here </a>
			
### Producing chess half-move images
From a <cite class='kw'>pgn</cite> chess file, using <cite class='kw'>rchess</cite>, we should be able to load the game, get the [FEN](https://fr.wikipedia.org/wiki/Notation_Forsyth-Edwards) string for each of its positions and to produce a ggplot to be saved under <cite class='kw'>png</cite> image format. Pay attention to not confuse <cite class='kw'>pgn</cite> and <cite class='kw'>png</cite>.  To do so, I'll use following R code, and use a short file I played with black side on <a href='https://lichess.org/'>lichess.org</a>
```R
fn <- file.path("~/pgn", '20180410_Chessmonkey1_vs_neonira.P4oDzgTw.pgn')
pgn <- readLines(fn, warn = FALSE)
pgn <- paste(pgn, collapse = "\n")
chsspgn <- Chess$new()
if (!chsspgn$load_pgn(pgn)) stop(paste('unable to load pgn file', fn))

moviepgn <- Chess$new()
pl <- chsspgn$history(verbose = TRUE)

rv <- sapply(0:nrow(pl), function(n) {
    if (n > 0) moviepgn$move(pl[n, 'san'])
    afen <- moviepgn$fen()
    z <- ggchessboard(fen = afen,
                      cellcols = c("#8ca2ad", "#dee3e6"),
                      perspective = 'black',
                      piecesize = 10)
    list(z)
  }, simplify = FALSE)

# a couple of convenient functions
ensureFilenameExtension <- function(fn, ext) paste0(sub(paste0(ext,'$'), '', fn, perl = TRUE), ext)
catn <- function(...) cat(..., '\n')

# a function to save a one or two plots to a single image, according to various layouts
s2png <- function(fn, p1, p2, tms = 0,  grid = FALSE) {
  tfn = ensureFilenameExtension(fn, '.png')
  png(filename = tfb, width = 1200, height = 622) # width must be even for ffmpeg to work fine
  if (!grid) print(p1)
  else
    if (!is.na(p2[1])) grid.arrange(p1, p2, nrow = 1) else grid.arrange(p1, nrow = 1)
  Sys.sleep(tms)
  dev.off()
  catn(fn)
  tfn
}


# produce images 
invisible(sapply(seq(length(rv)), function(i) {
    fn <- sprintf('png-%03d.png', i)
    s2png(fn, rv[[i]], NA)
}))

```
#### produced image samples
<img src='/images/games/d/png-005.png' width='600' alt='image #5 ' title='image #5'/>
<img src='/images/games/d/png-014.png' width='600' alt='image #14' title='image #14'/>
<img src='/images/games/d/png-015.png' width='600' alt='image #15' title='image #15'/>
		
So far, so good. We have now an image for each hal-move played in the original chess game. Just need to proceed to a quick movie montage to create a <cite class='kw'>.mp4</cite> video file. To do so, let's first create following <cite class='kw'>bash</cite> script. 

```bash
#!/bin/bash 
[ "${DEBUG}" = "${0##*/}" ] && set -x 

echo "creation mp4 movie"
ffmpeg -r 1 -i png-%03d.png -c:v libx264 -vf "fps=25,format=yuv420p" out.mp4 -y

[ "${DEBUG}" = "${0##*/}" ] && set +x 
exit 0
```
You have to save it into a <cite class='kw'>bash</cite> file and to run it, in the folder where you produced your chess half-move image files. This will produce a file named <cite class='kw'>out.mp4</cite>.  See below.  

<video height="400" controls>
  <source src="/images/games/d/demo.mp4" type="video/mp4">
 Your browser does not support the video tag.
</video> 

So, we just created a kind of standard video movie to display a chess game. Nothing really new, but it works fine, and most of all, it opens some opportunities of more advanced video montage.  

You'll ask why not using <cite class='kw'>animation</cite> R package. Just because, I experienced it several times and found it to be very slow, compared to bash script invocation. Just a matter of performance on my machine. Another reason, is that it helps in tracking issues. Here, it is easy to identify the issue. If it is a content issue, then it probably comes from <cite class='kw'>R</cite> processing. If it is a montage issue, it will probably have <cite class='kw'>ffmpeg</cite> as origin. If we were using <cite class='kw'>animation</cite> R package, resolving such issues won't be as easy. 

### Next part, to come 
We'll create a chessboard influence analysis system that will produce image showing influence zones on chessboard and that could display various interesting information to ease understanding of some chess moves. See you on part 3. 

##### Note
Images made using <cite class='kw'>ggplot</cite> R base package.  
Movie montage achieved by external shell script instrumenting <cite class='kw'>ffmpeg</cite> as it appeared to be much faster and reliable than thru <cite class='kw'>animation</cite> R package. 

