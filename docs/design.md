# :triangular_ruler: Design

Time to make a game!

Here's some tips for doing that.

## :seedling: Game Ethics

As with any creative medium, I feel it's important to be cognisant of the ethics of the product we develop. Unlike many other mediums, games have the addition of interaction, which opens a floodgate of concerns, especially relating to accessibility, and player psychology. However, I thought it would be good to talk a little bit about my experiences with AI, and some thinking I've done on the subject.

### Violence as a Tool, Violence as a Crutch

(Coming Soon) Concerning the bloated dead myths around 'videogame violence', but also violence as narrative, violence for aesthetics, and violence as a cultural fixation within the industry.

When people think of violence they usually think of head exploding gore, and the normalization of arcadey military deathmatches. I'm going to first give you a large number of extremely successful games which use violence in constructive or smart ways. This is just so we have a reason not to burn the whole house down before we get into conversation. I have marked stipulations and important context in **bolded text.**

1. The game uses violence to *punish, sicken, or scare* the player.
   1. This is often used to train the player about the mechanics.
   2. It's seen most commonly in genres like platformers, horror games, and stealth games.
   
* [Limbo](http://store.steampowered.com/app/48000/LIMBO/)
* [Alien: Isolation](http://store.steampowered.com/app/214490/Alien_Isolation/)
* [Outlast](http://store.steampowered.com/app/238320/Outlast/)
* [Thief: Deadly Shadows](http://store.steampowered.com/app/6980/Thief_Deadly_Shadows/)


2. The game is violent, but the player is expected to make a *deliberate choice* on whether to partake.
   1. Some of the best dialogues on game violence we started by a game itself critiquing our fixation on violence.
   2. Sometimes the choice to be non-violent isn't obvious, because players follow tropes blindly.
   3. The game mechanically punishes you or rewards you for your choice.
   4. The consequence carry weight because you *had the choice.*
   5. **As a designer, you must take into account representational consent with games where the player is given a choice to invoke violence against a depiction of a person. ([See next section.](#representation-identity-and-puppeteering))**
   
* [This War of Mine](http://store.steampowered.com/app/282070/This_War_of_Mine/)
* [Spec Ops: The Line](http://store.steampowered.com/app/50300/Spec_Ops_The_Line/)
* [Undertale](http://store.steampowered.com/app/391540/Undertale/)

3. The game's portrayal of violence is *realistic or frictional.*
   1. Weapons kill quick.
   2. Fights are dirty, and asymmetrical.
   3. Weapons don't feel like toys, but feel like tools.
   4. Allusion to or *direct simulation* of bystanders, civilians, and collateral damage.
   5. The violence enforces an aesthetic of authenticity, even education.
   6. **These games often begin as actual training simulators.**
   7. **These games are often unintentionally great 'Anti-War War Games'.**
* [DCS World](http://store.steampowered.com/app/223750/DCS_World/)
* [Arma 3](http://store.steampowered.com/app/107410/Arma_3/) which is a commercial version of [VBS3](https://en.wikipedia.org/wiki/VBS3)
* [Kingdom Come: Deliverance](http://store.steampowered.com/app/379430/Kingdom_Come_Deliverance/)
* [Rainbow Six 3](http://store.steampowered.com/app/19830/Tom_Clancys_Rainbow_Six_3_Gold/)

4. The game's violence enforces an aesthetic of *desperation and perserverance.*
   1. Physical or psychological in nature.
   2. Often the struggle is non-literal - metaphorical.
   3. Often the violence isn't the fun part - surviving is.
* [Hellblade: Senua's Sacrifice](http://store.steampowered.com/app/414340/Hellblade_Senuas_Sacrifice/)
* [Dark Souls](http://store.steampowered.com/app/211420/DARK_SOULS_Prepare_To_Die_Edition/)
* [Far Cry 2](http://store.steampowered.com/app/19900/Far_Cry_2_Fortunes_Edition/)
* [Darkest Dungeon](http://store.steampowered.com/app/262060/Darkest_Dungeon/)

5. Violence is the joke, *it's the message.*
   1. Satirical and overblown in nature.
   2. Commentary or critique on the Western fixation on violence.
   3. Often isn't set in the same universe as us, or is in an exaggeration of it.
   4. **This is the most often (in my opinion) wrongly-criticized form of violence in media, because the satire requires extensive knowledge of the thing it is satirizing. Media outlets often don't come from an angle of videogame literacy.**

* [Doom](http://store.steampowered.com/app/379720/DOOM/)
* [Viscera Cleanup Detail](http://store.steampowered.com/app/246900/Viscera_Cleanup_Detail/)
* [Borderlands](http://store.steampowered.com/app/8980/Borderlands/)
* [Hotline Miami](http://store.steampowered.com/app/219150/Hotline_Miami/)
* [Gang Beasts](http://store.steampowered.com/app/285900/Gang_Beasts/)
* [Grand Theft Auto V](http://store.steampowered.com/app/271590/Grand_Theft_Auto_V/)

6. Violence is the chosen channel for designed 'game feel'.
   1. Exaggerated player agency is the goal.
   2. Violence is the means.
   3. Players aren't chasing violence, but are rather are chasing agency.
   4. **Game Feel should not be leveraged against a group of people. The game must not depict violence against actual groups of people, or it gets into propaganda territory.**

...

### Representation, Identity, and Puppeteering

(Coming Soon) Concerning developing with sensitivity, a look at cultural appropriation, and the complications of representational consent of having a game avatar when the player is arbitrary.

### Exploitation, Whales, and Dice

(Coming Soon) Concerning predatory monetization, player behaviour, and gambling.

### Drawing Artificial Lines

(Coming Soon) Concerning artificial intelligence, humility, and my thoughts on how to approach development in burgeoning fields of intelligence emulation.

## :space_invader: Game Design

As a developer in a small team, you'll often have to make calls about design decisions when your designer is away for lunch, or even just because you're expected to know the answer. The basics of game design are more-or-less as follows:

### The Basics of Fun

1. Games are greater than the sum of their parts. 
    * If something isn't feeling good, add sound, animation principles, visual polish, agency, responsiveness, cinematography, tone, etc...
    * Good game developers can use the full spectrum of the medium to add flare and satisfaction to a part of a game.
    * GREAT game developers can make something look and feel good using only a couple of the aforementioned components.
2. Player input needs to be responsive.
    * It needs have have punch and it needs to feel good. 
    * If you need to slow the responsiveness of something down, use [animation principles](https://en.wikipedia.org/wiki/12_basic_principles_of_animation) to give it physicality. 
    * Dark Souls does this really well. Attacks don't happen instantly, but have anticipation, windup, followthrough, and there is a noticable secondary impact motion on the enemies which helps communicate your power.
3. Design toward an experience. Design by subtraction.
    * Everything in your game should bring it closer to a particular experiential aesthetic. Decide on that aesthetic early, and tailor EVERYTHING towards it.
    * Often the best way to make something better is to take something out of it. We make assumptions constantly about what 'should' be in a game. In the example of Zombie Donuts we let the player move around the environment, and due to the limitations of the Gear VR players didn't like the control scheme and felt sick because of it. Players had more fun by standing still.
    * If you want a great example of design by subtraction take a look at one of my favourite game designers of all time - Fumito Ueda's [Shadow of the Colossus](http://www.thesaint-online.com/2017/03/fumito-ueda-design-by-subtraction/) and [Ico.](https://www.youtube.com/watch?v=AmSBIyT0ih0)
4. Fuck tutorials.
    * If you can make a game entirely without tutorials, do it. 
    * In addition to forcing you to make a terrible bastardization of your gameplay loop, players hate them. 
    * Players hate reading, feeling patronized, and having the discovery of mechanics spoiled for them.
5. Teach the player without them noticing.
    * Use light or colour :rainbow: to guide the eye to important gameplay elements. 
    * Use sound to cue the player to look in a direction. Use framing to focus the player on important elements. 
    * Use visual weight (notice how the rainbow emoji draws your eye because it has a bolder visual presence than the rest of the text) to draw attention. 
    * Force the player using psychology to teach themselves how to play the game. It's hard but when it's done right it's phenomenal.

### XR-Specific

XR, which is a blanket term for VR, AR, MR (Mixed Reality) and other such designations, have some interesting design concerns associated with them, mostly around input and interaction. For those User Experience (UX) people out there, this might be interesting for you.

Here's a list of useful guidelines:

1. Make interactions kinetic! (Give them physicality and weight.)
    1. Have the player directly influence items in the game world or on the phone screen. 
    2. Don't rely on buttons and floating UI.
2. Avoid unmotivated movement, perspective shifts of any sort, and even movement in general if you can.
    1. Doing something like changing the Field of View in VR is such a no-no that most VR SDKs and APIs totally lock it.
3. Make intuitive or charming environmental interactions instead of buttons. 
    1. Ex. Toggle the music by having the player shoot a jukebox.

If you must do movement, try some of the following options:

1. Fade/blink to an indicated location.
2. **Slow** movement using conventional control schemes. Must be a decent controller with accurate directional and analog input.
3. Constant and linear movement. (See Run Dorothy Run)
4. Deliberate physical movement.
    1. Using motion controllers to swim or push off objects in space. 
    2. Needs to be tuned to feel physically true-to-life, make sure there are no physics glitches that will make you instantly barf. :mask:
    3. One game that does this REALLY well is [Lone Echo](https://youtu.be/zxPuZYMIzuQ?t=3457) which gets around this problem by having the player in zero-grav environments for the entirety of the game. You also see your body if you look down. Super cool.

## :camera: Case Studies

The best way to make good games is to play both good and bad games. Play a lot of them. Talk to friends about them. Analyze them.

### Shadow of The Colossus

(Coming Soon) Using feature subtraction, emptiness, scale, and grace, to evoke intense aesthetics.

### Dark Souls

(Coming Soon) Using adversity to enforce triumph. Forcing players to confront thoughtful play. Being okay with players missing a secret.
