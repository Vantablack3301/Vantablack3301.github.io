this was part of the january 2024 Gamecraft jam and it was the third one i participated in. at this point, i had already played with some premade post process shaders for the [previous jam](https://tsarcharchar.itch.io/power-punch) and felt like i was ready to experiment with making my own shaders. below you can see a demo i recorded in engine showcasing the enemy in the dark. 
![[2024-01-28 15-08-59.mp4]]

despite being for a game jam, a lot of the shaders actually came from a project i was working on months earlier. i was a fan of artist [*umami*](https://www.youtube.com/@abstractdaddy) and his work on projects like [Interface](https://www.youtube.com/watch?v=gdAbs95GIm4) and Safe Mode (particularly, the [Just Transition](https://www.youtube.com/watch?v=-mrVtRgbpAY) clip). its already an extremely interesting art style, and manages to have a unique way of bridging traditional 2d animation with more complicated 3d animations and setups. i was curious if it was possible to make something comparable in Unreal Engine.
![[2023-12-09 20-34-49.mp4]]

in the above clip, i still use an off the shelf VHS shader, but pretty much everything else was pretty standard. its made up of a Cel-Shader that does most of the heavy lifting, and an outline shader. you may or may not have noticed the pitch black sky, this comes from a bug in that outline shader. i have since lost the tutorial i was following to make the shader, but i liked the look enough that i figured it was worth keeping. making my personal project take place at night has a neat vibe to it.

after a while i managed to polish it up with some more details to give it the comic-y/graphic novel type look. mainly adding some hatching lines that became more notable on the brighter elements. much of that can be seen in the clip below.

![[2023-12-18 15-17-09.mp4]]