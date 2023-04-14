# JumpApp
An online didactic game for music training and education - paper submitted to ISMIR23

## Abstract
Musical learning is beneficial for individual of all ages.
In particular, the use of interactive software tools is considered nowadays essential for increased engagement, experience personalization, and effectiveness. This is particularly true for the task of music education, which has to face the problem of complex rules and notation. For these reasons, we developed JumpApp, a musical didactic game.
The devised software is a web application based on JavaScript, accessible through Chrome browser and no 
installation is required.
The objectives of JumpApp are twofold. First, the user is trained to improve the relative pitch with an engaging listening experience. Secondly, such a learning is decoupled from the classic music notation, through a user-friendly interface that maps notes in an octave in an innovative way, thus avoiding the learning of complex theoretical rules and musical notation of intervals and scales.
The quality of experience, versatility and learning effectiveness of JumpApp, has been evaluated by musicians with different music background through a questionnaire.
The paper is structured in a top-down fashion. We start from a description of the features of JumpApp. We then discuss how these features have been implemented in the software and the signal processing blocks that attain the goal. Finally, results of the evaluation process are reported along with final considerations and future works.

## Why?
This project is based on the idea of creating a fun, educational and musical game, available online for free, without the need to install it on your device.  
There are several applications related to ear training, but few (or none) related to the training of singing and of the relative pitch.  
JumpApp manages to do this, but in the form of a game!  
You can also play with a musical instrument in order to train a "sight-reading" that frees you from the musical notation.

## Game instructions
#### Settings
Two modalities of the game are available: static and progressive.  
The first one allows you to train on a specific scale that you can choose between the seven modes of the major scale.  
The second one (for the more experienced) provides a progressive increase in difficulty of the game: at each change of game level, the modal scale of reference changes with a colored match of the grid that shows the new scale.  
Before starting to play, the user can decide the octave range between note C2 to B5 on which he will play.

#### Play
The game consists in jumping on each platform to avoid dropping the avatar.  
The platforms are arranged on eight levels corresponding to the octave of a musical scale: from the most grave to the most acute, from the bottom to the top.  
The game background has vertical lines that emphasize the beats of a time in 4/4.  
You must sing the note corresponding to the next platform just before the avatar falls down (so in time with the grid). In the game there are also musical pauses identifiable by the lack of platforms: in this case you have to be silent and wait for the avatar to fly to the next platform to sing.

This release has not been tested for Apple Silicon CPU.

## How does it work?
The code is divided into several [modules](https://github.com/jumpapp-repo/jumpapp/blob/master/modulesUML.png) that cooperate together:  
  * PitchDetector
  * ScaleMapping
  * Graphics
  * Settings
  * Rhythm

The graphics module manages the graphical logic: the creation and movement of the platforms, the displacements of the avatar, the updating of the background based on the change of game levels, the control and management of the game over. The creation of the platforms includes the rhythm module that statistically models the choice of the duration of the notes and the use of the main musical patterns.   
When the user starts playing, the pitchDetector is listening on the microphone of the device and as soon as a change of pitch is detected it calculates the note detected and sends it to the scaleMapping module which compares the note played with the current musical scale of the game. Then the scaleMapping module sends a message to the graphics module: if the note is part of the scale it sends the platform number to which the avatar should jump, otherwise it sends an error. The graphics module will be able to understand if the avatar can jump on time in the next platform or if it will die.

## External libraries
For JumpApp development, the following external libraries have been used:
  * [Phaser3](https://phaser.io/phaser3): a framework used for managing graphics
  * [AubioJS](https://github.com/qiuxiang/aubiojs): a translated version of the Python [aubio](https://aubio.org) library in JavaScript used for the pitch detection
  * [Audiosynth](https://github.com/keithwhor/audiosynth): a dynamic waveform audio synthesizer used for the sound reproduction

## Demo
You can see a small [video demonstration of the game](https://jumpapp.surge.sh/demo_JumpApp.mp4) or the [complete version](https://jumpapp.surge.sh) where you can play.
#### Enjoy your time!

## Try it locally
If you want to try the game locally, you should:
1. Clone the repository: `git clone https://github.com/jumpapp-repo/jumpapp.git`
2. Move into the project directory: `cd jumpapp`
3. Start a local http server using python 3: `python -m http.server`
