---
layout: post
title:  "Poco Apollo"
date:   2018-03-29 12:40:17 +0000
categories: project generative
cover_photo: /assets/img/poco-apollo.jpg
excerpt: 'Online music composition, using generative algorithms to create short music pieces '
---

Poco Apollo is a generative music piece by Icelandic musician/programmer Halldór Eldjárn. It is built upon NASA’s photo archive from the Apollo Space mission, which consists of ~15.000 photos taken during the missions. The piece is a web app that generates musical soundscapes for the images in the library. It uses common computer vision algorithms to determine the mood of the picture and that is used as the input to the music composition engine.

You can check it out now: [pocoapollo.hdor.is](https://pocoapollo.hdor.is)

I created the piece to open up this incredible photo library. The mood in the pictures is somewhat unusual as some pictures look quite casual unlike the most famous and polished pictures we are so used to seeing, from these missions. Some are even quite bad, but still they are taken during one of the most incredible journeys mankind has embarked upon. The web app selects a picture at random and the browser then starts playing the soundtrack for that picture. 

All composition and audio is done in the browser. No data is downloaded from server except for the images and code to run the page. It is a joint effort of computer vision library Tracking.js and audio rendering with Tone.js, with some highly specific generative musical composition code bridging the two. 

The generative part is the heart of the piece. I took a decision early on to boil the whole image down to one parameter, which I call ‘mood’. Mood is determined by number of recognised sharp edges in the photo. The more busy the photo is, the higher the ‘mood’ parameter, the ‘happier’ the music sounds. One of the things that are chosen with the ‘mood’ parameter is the musical scale in which the song is played in. Lower ‘mood’ parameter yields more dissonance in the harmonies. This was all carefully handpicked by me to my preference and is not very scientific at all. 

Chords and chord progressions are created by iterating over a simple 7x7 cellular automata. Each field in the cellular automata has an assigned note from the scale, and the notes are distributed to favour larger intervals over smaller; Each cell has somewhat ‘nice sounding’ adjacent cells. 

I used a seeded random function, and use the unique image name as the seed so an image is always paired with the same piece. Revisiting an image at a later time will end up with the same result as before. This emphasizes that the whole piece contains ~15.000 short pieces.

Tone.js is an incredibly nice library to work with and you easily get lost in creativity. It is built on the Web Audio API and makes programming interactive synths and experiences in the browser a breeze, and it comes with a very comprehensive bank of code examples and a killer API documentation. My first attempt was to use a semi-abandoned library called Flocking.js, which is architected like the popular music programming engine Supercollider, and is declarative in nature. Patches easily got overly complicated to maintain due to JavaScript object nesting patterns and implementation of the library itself was sadly buggy, often producing some very hard to debug eardrum piercing glitches and screams. It took me 3 days to rewrite the whole piece with Tone.js *and* add many more features, compared to maybe a month with the other. But I sure hope Flocking.js will see some updates in the future, as it is still a very nice library but just did not fit this project very well. Tone.js is also loaded with Transport support, for playing and pausing and also provides sample accurate scheduling! 

All in all, it was a very enjoyable ride, to get acquainted with these technologies and how fun it is to finally have finished this piece which has just been an idea at the back of my head for quite some time now! I recommend putting your headphones on, turn the lights off and enjoy some space-y soundscapes at [pocoapollo.hdor.is](http://pocoapollo.hdor.is) .
