this was the first jam of the 2024-25 school year, and we had some big plans to do what we called "the megateam". while our 30 person jam team didnt end up realizing, we still had enough people to get rather ambitious with our idea.

since we were able to more evenly divide out the workload, we had a lot of people doing individual 2d art, 3d art, and engineering, and i want to give a shoutout to those people. their official credits are listed in the itch.io page. for my specific role, while i did still do some 3d art, i was more focused on shaders and the general look and feel of the whole game. on top of that, we had much better 3d artists on the team, so i was more concerned with some simpler models and a lot of the texture work.

![[Pasted image 20250123105036.png]]

as for the shader work, we knew from planning that we wanted to go for the PSX art style. so i initially tasked myself with breaking down the PSX style into various elements i could try to recreate in engine. and i was able to gather the following from it:
- lower resolution textures due to smaller ram/file size constraints
- fewer used colors (57,344 (256×224) to 153,600 (640×240) colors on screen)
- affine texture mapping resulting in that bendy and warped look of larger surfaces
- vertex jitter making things look sorta shaky at times
- lower resolutions thanks to the available televisions of the late 90s
so with that, it came down implementing each one as an individual element. while i could've probably found a tutorial to do all of this in one go, id much rather tackle each one manually and try to figure out how they worked.

the first one was affine warp. this came mostly from the affine texture mapping method not properly taking into account the depth of a plane and just warping and mapping the triangles individually. i was able to find a[ forum post](https://forums.unrealengine.com/t/how-can-i-simulate-affine-texture-mapping/359388/4) where they were discussing how to make an affine warp shader in unreal. i still don't understand the math as well as i understand the general concept, so it was mostly following their premade nodes, but i eventually had something decent looking down. the main change i made was converting it to a material function so i could combine it with other shaders.

![[Pasted image 20250123110438.png]]

after that it came down to recreating the vertex snapping/jitter that the PlayStation had. if the research i did still tracks, it came from the psx rounding vertex positions to integers rather than being true floating point numbers, so they would snap to the nearest hard int instead of moving smoothly in the world space. the guide i used when following most of this shader used global parameters to define the 3d grid size, which was then used in a simple rounding node setup to snap the vertices to the divided points of the 3d grid. this was also simplified into a material function that could easily be plugged into the world offset of the material output. this meant just three nodes including the image texture to get the most recognizable parts of the PSX look.

![[Recording 2025-01-23 145230.mp4]]

on a related note, i also had to do a bit of work on getting textures to look aesthetically in line. the PlayStation 1 used pretty low resolution textures, and didn't have any filtering to make things look blurrier. for me to replicate this, i had to bring all the models into blender, then export their properly UV'd albedo texture at a significantly lower resolution (on average, between 10x and 5x depending on the existing scale). this got most of the look right in the textures themselves, but unreal had an annoying habit of filtering. gone were the crisp individual pixels i saw in blender and IrfanView, and in its place was a blurry sludge that made things pretty unrecognizable. the version of unreal we were using didn't support no filtering either, so the closest solution was to use nearest neighbor filtering. while this did work pretty well, and may even pass to the untrained eye, it did have the negative downside of me getting roasted by a professor i showed it to. not much i can do now though.

![[Pasted image 20250123145922.png]]

the last things i had to do at this point was lowering the color space, and pixelating the game. while just lowering the game resolution was a valid choice to do, that was more of an engineering related task that i didn't really have a ton of time to figure out. so instead i found a tutorial for a basic pixelation shader. this method did require the pixel size to be hardcoded, but since we were targeting 1080p we just decided to stick with that.

![[Pasted image 20250123150312.png]]

as for the limited color space, this wasn't technically a huge issue on the PSX at the time. it supported a maximum color depth of 24 bits (comparable to most modern consumer displays), which is more than enough for all but very dark scenes without having any color banding. and because the dominant display technology of the time, CRT TVs, were analogue, there wasn't any way of actually having this kind of limitation on a console like that back in the day. but i decided that the look not only added to the heavily dated style we were after, but when i finished the effect it also kind of looked like a busted CRT that would mess up some of the colors it was outputting. this effect once again involved some math i still don't fully understand, but it a fairly quick process to set up. and the result definitely had that lack of color people from the early early internet recognize.

![[Pasted image 20250123161755.png]]

the end result took a lot of effort to set up with all the individual assets, but i am quite happy with how it turned out. it has that retro look to it that works extremely well, even if its not entirely faithful to the PSX. and while i obviously could've polished things up if i had more than a weekend to do this,  I don't think I actually would've changed much.

![[2025-01-03 13-52-55.mp4]]