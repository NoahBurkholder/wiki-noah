# :sparkling_heart: Wiki Noah

## Version 1.4.4 (Sparkling Heart) - March 14th, 2018

# :question: Ok, what the fuck is this, Noah?

In short, this is a **Practical Resource For New Game Developers**. It is also a **Case Study for Students Entering Game Dev**, a **Reminder to Myself That What I Do Is SUPER COOL**, and hopefully a **Place to Share Passions and Expertise**.

Basically, at work I've been writing a bunch of documentation for Git, Unity, C#, Game Design, and just general industry stuff and useful shit for game developers and dev-adjacent people. It was meant for onboarding co-op students who are still in school and need a big, easy to understand overview of some practical development concepts.

I showed it to Minh when I got home one day and he was super stoked about everything that was on here and wanted me to send him a copy (Hi Minh!). Figured I'd basically just make this public to help out anyone who might be interested, or at least give an interesting read about the kind of work I'm doing.

# :wave: Welcome

Welcome to my Wiki repository to which you are reading. I will be updating this relatively often with new stuff I learn through practical work at my job, as well as things I've learnt from the various senior developers I talk to at game dev meetups.

### Getting Started

Okay. *Don't freak out* is my first advice. The most unanimous feeling in all of game development is crippling imposter syndrome.

> "Impostor syndrome (also known as impostor phenomenon, fraud syndrome or the impostor experience) is a concept describing individuals who are marked by an inability to internalize their accomplishments and a persistent fear of being exposed as a 'fraud'."

[- Wikipedia](https://en.wikipedia.org/wiki/Impostor_syndrome)

The truth is even the most beginner programmer is only a few months hard work from being a game-industry-professional. When I first talked to a professional in the field, I was able to comprehend what they were talking about, even after just learning the basics of polymorphism. It's not unattainable.

> Everyone is struggling to push their own boundaries, and they're only struggling because nobody teaches anyone else shit.

[- Me, I said this.](#getting-started)

Now, by working as a game developer, you're also a game designer. You will need to make on-the-fly calls about what is best for the player's experience. **For this reason, one of the most important reads for you is [The Basics of Fun](development.md#the-basics-of-fun).** This is perhaps the most valuable one-pager you'll read on the wiki, because it will affect how you do *everything* during development. It's based on a soft understanding of various famous works including Steve Swink's ["Game Feel"](https://en.wikipedia.org/wiki/Game_feel) as well as analysis of some of my own favourite games, and what makes them tick.

I recommend taking the time to learn [good protocol surrounding Git](git.md#repository-protocol), as well as refresh yourself on [the basics](git.md#-git-basics). This is especially important since I'm going to talk about Git using the commandline interface. There is no guess-work involved, and there aren't any confirmation boxes saying *"ARE YOU SURE?"*. This is mostly because it's how I learnt Git, but it comes with the added benefit of feeling like a hacker-wiz, and you also gain a better understanding of the underlying operations simply because each command is deliberate by nature of the command prompt.

Additionally, on this Wiki there is a boatload of fantastic and less-than-obvious tips, tricks and tools relating to [Unity](development.md#-unity) and [C#](development.md#-code) which I have poured my souls (plural) into.

If you're relatively new to the game development field this Wiki is for you. If you went to school with me in SIAT then this Wiki is for you. It doesn't teach you the basics of programming (yet), but it gives you enough extra knowledge that you can rub shoulders with seasoned developers. I know - I was surprised too.

Frankly, since I wrote this for fellow coworkers in software development positions, it skips a lot of the basics of coding, and that is something I hope to remedy in the future when I have more time. Let me know what concepts in particular - fundamental or otherwise - you'd like covered and I'll prioritize those first.

### My Favourite Topics

Okay. Now let's dive in. I'm going to point to a few of my favourite sections which you won't necessarily be stoked about or even understand, but maybe there's a spark in there. Maybe you'll understand something.

1. [The Basics of Fun](development.md#the-basics-of-fun)
2. [Scrutinize Your Commit Messages](git.md#scrutinize-your-commit-messages)
3. [Unity Best Practices](development.md#best-practices)

# :bookmark_tabs: Table of Contents

In order of execution.

## :truck: Logistics

### :moneybag: [The Industry](industry.md)

1. [:thumbsup: The Pros](industry.md#-the-pros)
    1. [Community](industry.md#community)
    2. [Dreambuilding](industry.md#dreambuilding)
    3. [Transferability](industry.md#transferability)
2. [:thumbsdown: The Cons](industry.md#-the-cons)
    1. [Hollywood Has It Easier](industry.md#its-impossible)
    2. [Job Security Who?](industry.md#job-security-who)

### :file_folder: [Git](git.md)

1. [:baby: Git Basics](git.md#-git-basics)
    1. [How does it work?](git.md#how-does-it-work)
    2. [What is a commit?](git.md#what-is-a-commit)
    3. [Okay, so what does the repository look like on my computer?](git.md#okay-so-what-does-the-repository-look-like-on-my-computer)
    4. [Committing + Pushing](git.md#committing-pushing)
    5. [Pulling](git.md#pulling)
    6. [Checkout](git.md#checkout)
    7. [Scrutinize Your Commit Messages](git.md#scrutinize-your-commit-messages)
    8. [Merging](git.md#merging)
2. [:japanese_ogre: Advanced Git](git.md#-advanced-git)
    1. [Repository Protocol](git.md#respository-protocol)
    2. [Feature/Issue Branching Methodology](git.md#featureissue-branching-methodology)
    3. [Resolving Conflicts Manually](git.md#resolving-conflicts-manually)

## :wrench: Development

### :coffee: [Code](code.md)
1. [:musical_score: C#](code.md#-give-me-link)
    1. [Singleton Managers](code.md#singleton-managers)
    2. [Coroutines](code.md#coroutines)
    3. [Enumerators](code.md#enumerators)

### :dragon: Shaders
1. [:ant: CG](shaders.md)
    1. [Coming Soon](shaders.md)


### :game_die: Unity
1. [:game_die: Unity](unity.md#-unity)
    1. [Unity Timesavers](unity.md#unity-timesavers)
    2. [Reference IDs](unity.md#reference-ids)
    3. [Know the Costs of Unity Methods](unity.md#know-the-costs-of-unity-methods)
    4. [Take Update Loops Seriously](unity.md#take-update-loops-seriously)
3. [:factory: Building](building.md)
    1. [The Basics](building.md#the-basics)
    2. [The Output](building.md#the-output)
    3. [Building for Android](building.md#building-for-android)
4. [:chart_with_upwards_trend: Optimization](optimization.md)
    1. [The Basics](optimization.md#the-basics)
    2. [Noah's Hit-List](optimization.md#noahs-hit-list)

### :seedling: Design

1. [:seedling: Game Ethics](design.md#-game-ethics)
    1. [Violence](design.md#violence)
    2. [Representation](design.md#representation)
    3. [Exploitation](design.md#exploitation)
    4. [Artificial Intelligence](design.md#artificial-intelligence)


1. [:space_invader: Game Design](unity.md#game-design)
    1. [The Basics of Fun](unity.md#the-basics-of-fun)
    2. [XR-Specific](unity.md#xr-specific)



# :black_nib: Authors

[**Noah Burkholder**](https://www.linkedin.com/in/nburkhol) - [http://noahburkholder.com](http://noahburkholder.com)  
[Your Name Here]

## :pray: Acknowledgments
I'd like to thank Google, as well as the following individuals:

- [Tony Pacheco](https://www.linkedin.com/in/tony-pacheco/) - Who helped me write up the initial Wiki materials you're reading, especially around Git Methodology and Building. He's really good at sword fighting.

- [Minh Buinhat](https://www.linkedin.com/in/nhatminh-bui-a2407573/) - Who reminded me that maybe some people can relate to my passions and would benefit from anything I can teach. Discovered he could ask me about Unity and I would give him 3 hour long tutorials.

- [Logan Buchanan](https://www.linkedin.com/in/logan-buchanan-90b8b3126/) - Who encouraged me to the point I'm comfortable sharing this Wiki. He basically got me through school, whether he knows it or not.

As well as [Meri](https://www.linkedin.com/in/meri-morganov-43818a21/), Stephanie, [Andy](https://www.linkedin.com/in/hao-tang-90947413b/), [Helen](https://www.linkedin.com/in/helen-terry/), and [Bryan](https://www.linkedin.com/in/bryanshen/) for being my first partners in crime.
