# What is even this sussy project?! XD

Simply put, this is a web application of a pixelated canvas drawing board XD. The tiny little thing is made in Vue framework, which is a fitting choice due to how simple the framework is. 
The unexpected thing about this project is that it's actually fun: the doing process and the thing itself. Perhaps my best personal made project so far XD!
Instead of going on and on, I think you should try out the app and see it for yourself: 

# The making process

The app is made (other than the obvious choice of Vue.js) using browser's built-in canvas API. 
The ability to draw a pixel beneath the tip of your cursor is composed of the canvas API's fundamental function .fillRect (which belongs to .getContext('2d')), combined with some basic event handlings that detect the position of your cursor, your clicking, and so forth.

Other than Vue's core library imports, this project doesn't use any external libraries.
The project however does notably uses the SCSS preprocessor. It's worth saying how really useful SCSS is, even just its ability to nest child stylings and explicitly apply the CSS effects on only either the parent or the inheritor. To the point it made me even wonder how come SCSS isn't even some sort of industry standard or widely used. But perhaps maybe it used to be? A lot of time has passed and Tailwind is now the new standard thing, so perhaps it's not really a wonder why - each thing still has their own niche use cases still.

Assets for the sound effects are downloaded from Pixabay - needless to say, those sound effects are not my original creations, and none of them will be used for any commercial purpose.

The icon (showed on the tab) is originally made by me :).

# Is that it?

Originally, I wanted to add some sort of music player (maybe lo-fi music) on the app, and the ability to let multiple users draw on the board in real live time. But I don't have more time for this project than I can afford to allocate them on it, so as of now these are just plans.

Perhaps also worth being noted is how during the course of making this app, I realized how it can be made into really fun games (battleship types, minesweepers, drawing-matching, etc). These ideas have some potential and perhaps it would be great if I can realize them in the future somehow. 

# The needful

In case you want to try it out locally.
Or, maybe the deployed site is down.
Whatever reason it is, here are the command lines to make it run after cloning this project:

```
cd <project's directory>\miniBoard
npm install
npm run dev
```

Note: Make sure you have installed Node.js before running the commands. 