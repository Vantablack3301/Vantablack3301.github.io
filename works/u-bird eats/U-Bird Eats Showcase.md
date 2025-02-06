oIn November of 2024, I participated with a team in the final game jam for the semester as part of the U of Us game development club, Gamecraft. The theme for the jam was 'Wing it', which of course led us to the idea of making a game based on a bird doing uber eats orders. While i built up a name as a technical artist for almost all of my previous game jams, i was the only one with engineering skills for this jam so i served as the teams engineer.

<video controls src="ubird-eats.mp4" title="Title"></video>

Probably the most difficult part about all of this was making a character controller with a jetpack. I've already become too used to standard first and third person controllers, which at least helped get a baseline horizontal movement system going. But it took a few hours of experimentation but i eventually settled on one that disabled gravity and added an upwards force to the character whenever space was pressed, and reset gravity to normal when it was released. ![](<jetpack script.png>)

given our significantly smaller team and more limited resources, we opted to design a simple gameplay loop around picking up an order from the restaurant and delivering it to a randomly chosen house. this loop was extremely easy to implement as we simply had to have a house game object that would be automatically grouped into a list in the game mode. you then just had to randomly pick one to deliver to, and pick again whenever players returned to the restaurant.

{the code was too long to sensibly share a screenshot, so ill share a link to the repo once this goes live}

despite being the engineer, i still did some shader work for the project. that of course was the objective highlighter. for a large map, we needed some way to show the player where they had to go. on top of having somewhat limited UI knowledge, i felt like standard UI could easily become cluttered. the ideal solution to this was to highlight the building geometry itself. my first attempt involved just setting the building to the maximum possible brightness. this went about as expected.

![](<Pasted image 20250106143301.png>)

not only was it not really all that visible in the scene, our cell shader (made by the very talented austin) didn't really handle emissive color all that well.

the next approach was to use a custom stencil shader that overlayed a bright color on top of the screen in post processing. this ended up being significantly easier as i was able to reuse a shader i had made previously for the Pizza Hunt jam for a similar outline, but edit it to be the whole object instead of an outline. 

![](<Pasted image 20250106144208.png>)

at the last minute, we ended up deciding as a team that there should be smaller optional collectibles the player can pick up on the way that increases their total earnings in the game. while they weren't hard to program, we did have to deal with the task of scattering them throughout the map. initially, one of our designers hand placed them around the initial spawn zone. this worked okay, but wasn't ideal for obvious reasons. as an alternative, i made a custom function that randomly placed 50 chicken wings within the bounds of the map. to get these bounds, i placed a temporary cube and moved it to the edges of the map to get some general minimum and maximum coordinates it could spawn at. 
![](<Pasted image 20250106150114.png>)

at this point, we had roughly an hour until submission. so while the rest of the team was putting together some final menus and an Itch.io page for it, i polished a few things up here and there. mainly by implementing some basic UI for stats and timers as well as adjusting the timer to not count down when you completed an order. the final result is available to download on windows for free from itch.
https://exudos.itch.io/u-bird-eats