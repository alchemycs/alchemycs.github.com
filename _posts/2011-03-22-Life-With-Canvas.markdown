---
title: Life With Canvas
layout: post
---

The `canvas` element has been around for a while now on webkit and has
made it into HTML5. I have never had the chance to use it, so I
thought I would give it a go by implementing that 'ol favourite, [Conway's Game of
Life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life).

I wrote my first implementation of it years ago on my C=64 in BASIC
using `peek` and `poke` directly to the screen
memory...ahhh...memories...

So here is a pretty basic version written in Javascript for the
`canvas` element. What I love about life is how simple the algorithm
is, but how hypnotizing the effect can be! 

Writting this again made me feel all warm and fuzzy inside with my
memories harkening back to a more innocent time when I coded for fun and not for profit!

The source can be found inside my [Playground GitHub
repository][playground]. 

<div>
<button id="reset">Reset</button>
<button id="startStop">Go</button>
<canvas width="400" height="400" id="life" style="border: 1px solid #999999;">
Sorry, your browser doesn't support the canvas element. Try using Firfox, Safari, Chrome or Opera.
</canvas>
<script src="https://github.com/alchemycs/Playground/raw/master/life/life.js"></script>
</div>

[playground]: https://github.com/alchemycs/Playground
