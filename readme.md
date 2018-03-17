# :cyclone: Wiki Noah

## Version 1.5.1 (Cyclone) - March 17th, 2018

# :question: Ok, what the fuck is this, Noah?

<details><summary> In short, this is a <b>Practical Resource For New Game Developers</b>. It is also a <b>Case Study for Students Entering Game Dev</b>, a <b>Reminder to Myself That What I Do Is SUPER COOL</b>, and hopefully a <b>Place to Share Passions and Expertise</b>. (Click to expand.)</summary><br>

Basically, at work I've been writing a bunch of documentation for Git, Unity, C#, Game Design, and just general industry stuff and useful shit for game developers and dev-adjacent people. It was meant for onboarding co-op students who are still in school and need a big, easy to understand overview of some practical development concepts.

I showed it to Minh when I got home one day and he was super stoked about everything that was on here and wanted me to send him a copy (Hi Minh!). Figured I'd basically just make this public to help out anyone who might be interested, or at least give an interesting read about the kind of work I'm doing.
</details><br>

# :wave: Welcome

Welcome to my Wiki repository to which you are reading. I will be updating this relatively often with new stuff I learn through practical work at my job, as well as things I've learnt from the various senior developers I talk to at game dev meetups.

### Icebreaking, or How I Learned to Stop Worrying and Love the Game

<details><summary>Okay. <i>Don't freak out is my first advice.</i> (Click to expand.)</summary><br>

The most unanimous feeling in all of game development is crippling imposter syndrome. 
    
I have literally never heard someone in Game Development say they don't feel feelings of inadequacy. It's almost just assumed *of and by everyone.* So much so, that developers will often talk to you about how they're fighting their feelings of inadequacy *before talking to you about their game.* It's kinda just a good icebreaker, honestly. Guaranteed common ground, and one of the many reasons game developers [have eachother's backs.](industry.md#community)

> "Impostor syndrome is a concept describing individuals who are marked by an inability to internalize their accomplishments and a persistent fear of being exposed as a 'fraud'."

[- Wikipedia](https://en.wikipedia.org/wiki/Impostor_syndrome)

The truth is even the most beginner programmer is only a few months hard work from being a game-industry-professional. When I first talked to a professional in the field, I was able to comprehend what they were talking about, even after just learning the basics of polymorphism. It's not unattainable.

> Everyone is struggling to push their own boundaries, and they're only struggling because nobody teaches anyone else shit.

[- Me, I said this.](#getting-started)
</details><br>
<details><summary>Now, by working as a game developer, you're also a game designer. You will need to make on-the-fly calls about what is best for the player's experience. (Click to expand.)</summary><br> 
    
**For this reason, one of the most important reads for you is [The Basics of Fun](development.md#the-basics-of-fun).** This is perhaps the most valuable one-pager you'll read on the wiki, because it will affect how you do *everything* during development. It's based on a soft understanding of various famous works including Steve Swink's ["Game Feel"](https://en.wikipedia.org/wiki/Game_feel) as well as analysis of some of my own favourite games, and what makes them tick.

I recommend taking the time to learn [good protocol surrounding Git](git.md#repository-protocol), as well as refresh yourself on [the basics](git.md#-git-basics). This is especially important since I'm going to talk about Git using the commandline interface. There is no guess-work involved, and there aren't any confirmation boxes saying *"ARE YOU SURE?"*. This is mostly because it's how I learnt Git, but it comes with the added benefit of feeling like a hacker-wiz, and you also gain a better understanding of the underlying operations simply because each command is deliberate by nature of the command prompt.

Additionally, on this Wiki there is a boatload of fantastic and less-than-obvious tips, tricks and tools relating to [Unity](development.md#-unity) and [C#](development.md#-code) which I have poured my souls (plural) into.
</details><br>
<details><summary>If you're relatively new to the game development field this Wiki is for you. If you went to school with me in SIAT then this Wiki is for you. (Click to expand.)</summary><br>

It doesn't teach you the basics of programming (yet), but it gives you enough extra knowledge that you can rub shoulders with seasoned developers. I know - I was surprised too.

Frankly, since I wrote this for fellow coworkers in software development positions, it skips a lot of the basics of coding, and that is something I hope to remedy in the future when I have more time. Let me know what concepts in particular - fundamental or otherwise - you'd like covered and I'll prioritize those first.
</details><br>
<details><summary>I have no plans of neglecting this wiki in the future, and I want this resource to grow based on <b>your</b> experiences and expertise too. If you have anything you'd like to add to this documentation, I'll add you as an author! (Click to expand.)</summary><br>
    
In general I'll only accept contributions if:

1. I've met you in real life.
2. You do creative stuff.
3. You're not an asshole.

But I think I can find a place for just about any topics, especially if they pertain to all creatives, and especially if the content is game-applicable. That said I don't want to limit this resource exclusively to games when so much of it is transferrable to other mediums.

If you're interested in contributing there are a few ways to do that, and I'm open to all of them:

1. Literally teach me something.
    1. I'll write my interpretation down for you!
    2. You'll get acknowledgement and thanks on the wiki!
2. If you're not comfortable using [Git](git.md) yet, just send me plain text!
    1. Super easy.
    2. I'll worry about adding you as an author, and any images and formatting!
3. Make a pull request!
    1. You get full control of the markdown (.md) files!
    2. Your name will be etched into the commit history and Contributors section!
    3. You're an author now too!
    
Thanks in advance, and I hope you'll join me in this little project.
</details>

### My Favourite Topics

Okay. Now let's dive in. I'm going to point to a few of my favourite sections which you won't necessarily be stoked about or even understand, but maybe there's a spark in there. There's a good chance it'll expand your understanding, even if most of it is putting the cart before the horse.

1. [:space_invader: The Basics of Fun](design.md#the-basics-of-fun)
2. [:octopus: What Makes Unity Great](unity.md#octopus-what-makes-unity-great)
3. [:baby: Git Basics](git.md#baby-git-basics)

# :bookmark_tabs: Table of Contents

## :truck: Logistics

### [:moneybag: The Industry](industry.md) (5% Complete)

1. [:thumbsup: The Pros](industry.md#thumbsup-the-pros)
    1. [Community](industry.md#community)
    2. [Dreambuilding](industry.md#dreambuilding)
    3. [Transferability](industry.md#transferability)
2. [:thumbsdown: The Cons](industry.md#thumbsdown-the-cons)
    1. [Hollywood Has It Easier](industry.md#hollywood-has-it-easier)
    2. [Job Security Who?](industry.md#job-security-who)

### [:file_folder: Git](git.md) (80% Complete)

1. [:baby: Git Basics](git.md#baby-git-basics)
    1. [How does it work?](git.md#how-does-it-work)
    2. [What is a commit?](git.md#what-is-a-commit)
    3. [Okay, so what does the repository look like on my computer?](git.md#okay-so-what-does-the-repository-look-like-on-my-computer)
    4. [Committing + Pushing](git.md#committing-and-pushing)
    5. [Pulling](git.md#pulling)
    6. [Checkout](git.md#checkout)
    7. [Scrutinize Your Commit Messages](git.md#scrutinize-your-commit-messages)
    8. [Merging](git.md#merging)
2. [:japanese_ogre: Advanced Git](git.md#japanese_ogre-advanced-git)
    1. [Repository Protocol](git.md#repository-protocol)
    2. [Feature/Issue Branching Methodology](git.md#featureissue-branching-methodology)
    3. [Resolving Conflicts Manually](git.md#resolving-conflicts-manually)

## :wrench: Development

### [:triangular_ruler: Design](design.md) (30% Complete)

1. [:seedling: Game Ethics](design.md#-game-ethics)
    1. [Violence as a Tool, Violence as a Crutch](design.md#violence-as-a-tool-violence-as-a-crutch)
    2. [Representation, Identity, and Puppeteering](design.md#representation-identity-and-puppeteering)
    3. [Exploitation, Whales, and Dice](design.md#exploitation-whales-and-dice)
    4. [Drawing Artificial Lines](design.md#drawing-artificial-lines)

2. [:space_invader: Game Design](unity.md#-game-design)
    1. [The Basics of Fun](unity.md#the-basics-of-fun)
    2. [XR-Specific](unity.md#xr-specific)

3. [:camera: Case Studies](design.md#-case-studies)
    1. [Shadow of The Colossus](design.md#shadow-of-the-colossus)
    2. [Dark Souls](design.md#dark-souls)

### [:game_die: Unity](unity.md) (75% Complete)
1. [:octopus: What Makes Unity Great](unity.md#octopus-what-makes-unity-great)
    1. [Live Updates](unity.md#live-updates)
    2. [Inspector Gadget](unity.md#inspector-gadget)
    3. [The Profiler](unity.md#the-profiler)
    4. [Reference IDs](unity.md#reference-ids)
    5. [Multiplatform as Hell](unity.md#multiplatform-as-hell)
2. [:violin: Best Practices](unity.md#violin-best-practices)
    1. [Know the Costs of Unity Methods](unity.md#know-the-costs-of-unity-methods)
    2. [Take Update Loops Seriously](unity.md#take-update-loops-seriously)
    3. [Unity Timesavers](unity.md#unity-timesavers)
3. [:factory: Building](building.md)
    1. [The Basics](building.md#the-basics)
    2. [The Output](building.md#the-output)
    3. [Building for Android](building.md#building-for-android)
4. [:chart_with_upwards_trend: Optimization](optimization.md)
    1. [The Basics](optimization.md#the-basics)
    2. [Noah's Hit-List](optimization.md#noahs-hit-list)

### :coffee: [Code](code.md) (50% Complete)
1. [:musical_score: C#](code.md#-give-me-link)
    1. [Singleton Managers](code.md#singleton-managers)
    2. [Coroutines](code.md#coroutines)
    3. [Enumerators](code.md#enumerators)

### :dragon: Shaders (3% Complete)
1. [:ant: CG](shaders.md)
    1. [What is this? A Language For Ants?](shaders.md#ants)
    2. [CG Structure](shaders.md#cg-structure)
        1. [Deferred vs. Forward Rendering](shaders.md#deferred-vs-forward)
        2. [Papa's Proper Use of Properties](shaders.md#properties)
        3. [Subshader? I Barely Knew Her!](shaders.md#subshaders)
        4. [Falling Back](shaders.md#falling-back)
    3. [Shading](shaders.md#shading)
        1. [NdotL](shaders.md#ndotl)
        2. [Light Processing](shaders.md#light-processing)
        3. [LUTs](shaders.md#luts)
        4. [Matrix Multiplication](shaders.md#matrix-multiplication)
        5. [Viewing Angles](shaders.md#viewing-angles)
        6. god there's gonna be a lot in here eventually
    4. [Case Studies](shaders.md#case-studies)
        1. [Cel Shading](shaders.md#cel-shading)


# :black_nib: Authors

[**Noah Burkholder**](https://www.linkedin.com/in/nburkhol) - [http://noahburkholder.com](http://noahburkholder.com)  
[Your Name Here]

## :pray: Acknowledgments
I'd like to thank Google, as well as the following people:

- [Tony Pacheco](https://www.linkedin.com/in/tony-pacheco/) - Who helped me write up the initial Wiki materials you're reading, especially around Git Methodology and Building. He's really good at sword fighting.

- [Minh Buinhat](https://www.linkedin.com/in/nhatminh-bui-a2407573/) - Who reminded me that maybe some people can relate to my passions and would benefit from anything I can teach. Discovered he could ask me about Unity and I would give him 3 hour long tutorials.

- [Logan Buchanan](https://www.linkedin.com/in/logan-buchanan-90b8b3126/) - Who encouraged me to the point I'm comfortable sharing this Wiki. He basically got me through school, whether he knows it or not.

As well as [Meri](https://www.linkedin.com/in/meri-morganov-43818a21/), Stephanie, [Andy](https://www.linkedin.com/in/hao-tang-90947413b/), [Helen](https://www.linkedin.com/in/helen-terry/), and [Bryan](https://www.linkedin.com/in/bryanshen/) for being my first partners in crime.

Additionally I want to thank [IndiePod](http://www.indiepod.org/) in Vancouver for being an endless source of knowledge, inspiration, community, and talent. I wouldn't consider this Wiki valuable if I hadn't learned a lot of it from you all.
