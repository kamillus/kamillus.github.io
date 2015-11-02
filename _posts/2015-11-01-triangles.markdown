---
layout: post
title:  "Sierpinski Triangles.. Square?"
date:   2015-11-01 22:52:20
categories: algorithms,recursion
---

Being bored is a powerful motivator for doing cool stuff. I was reading about Sierpinski's triangles and decided to do my own spin on them. Using js with tail end recursion and the html canvas element I was able to accomplish the following:

<img src="/images/output.png">

The code is fairly straightforward, however, I will have to admit that getting the positioning right in my head was a little bit of a challenge.


	<html>
	<head>
	</head>
	<body>
	<canvas id="c" width="500" height="500">
	</canvas>
	</body>
	<script>
		var c = document.getElementById("c");
		var ctx = c.getContext("2d");

		var vals = {x: 500, y: 500, width: 500, height: 500}
		ctx.rect(vals.x-vals.width,vals.y-vals.height,vals.width,vals.height);
		draw_lines({x: 250, y: 250, width: 250, height: 250}, 0)

		function draw_lines(vals, iter)
		{	
			if(iter > 6)
			{
				ctx.rect(vals.x-vals.width,vals.y-vals.height,vals.width,vals.height);
				ctx.rect(vals.x,vals.y,vals.width,vals.height);
				ctx.stroke();
				return;
			}		
	
			vals1 = {x: vals.x-vals.width/2, y: vals.y - vals.width/2, width: vals.width/2, height: vals.height/2}			
			draw_lines(vals1, iter+1);
	
			//vals2 = {x: vals.x+vals.width/2, y: vals.y -vals.height/2, width: vals.width/2, height: vals.height/2}
			//draw_lines(vals2, iter+1);
	
			vals3 = {x: vals.x+vals.width/2, y: vals.y+vals.height/2, width: vals.width/2, height: vals.height/2}
			draw_lines(vals3, iter+1);
	
			vals3 = {x: vals.x-vals.width/2, y: vals.y+vals.height/2, width: vals.width/2, height: vals.height/2}
			draw_lines(vals3, iter+1);
		}

	</script>
	</html>


The code only goes to the depth of 6; anything other than that was starting to choke my browser. I'm using rectangles to draw the figure instead of lines (I may be bored, but I'm also lazy). Anyway, I hope you enjoy this little piece of code.

