# :coffee: Code

## Singleton Managers
Any script called [Blank]Manager - ex. GameManager, PlayerManager, LevelManager, AudioManager - should probably use this convenient and safe setup. It allows you to access an instance from anywhere in the project by ensuring that a static reference to a singleton exists at all times.

A singleton pattern is a code pattern designed to ensure only one instance and always one instance of the script are available. These scripts are designed from the ground up to self-police.

```c#
public class GameManager : MonoBehaviour
{
    private static GameManager _instance;

    public static GameManager instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = (GameManager)FindObjectOfType(typeof(GameManager));

                if (_instance == null)
                {
                    Debug.LogError("An instance of " + typeof(GameManager) +
                        " is needed in the scene, but there is none.");
                }
            }

            return _instance;
        }
    }

    public void Awake()
    {

        // Check if instance already exists
        if (_instance == null)
        {
            // If not, set instance to this
            _instance = this;
        }
        // If instance already exists and it's not this:
        else if (_instance != this)
        {
            // Then destroy this. This enforces our singleton pattern.
            Destroy(gameObject);
        }
    }
}
```

## Coroutines

Coroutines are your new best friend. They are the polite cousin of the Update loops bundled with Unity.

Coroutines can patiently wait durations of time, and will function asynchronously - kinda like a pseudo thread - so that if they get held up, the rest of your code will continue to fly by. They are perfect for sequencing events in cutscenes, or doing large tasks over a dilute period of time.

You can make a custom loop which only updates every 20 seconds if you wanted to, or simply mimic the Update loop without hurting the buttery smoothness of your Camera transforms thanks to asynchronicity! :100:

As you'll discover, using `yield return` is one of coroutines' most powerful tools for sequencing and looping. You'll be using lots of `yield return WaitForSeconds(float)` so it's good to optimize them nicely using the following resource saver:  

```c#
// Create a reference to a single public Wait() object for each length of wait time you'll need. 
// Store this refernce in the GameManager script. Accessible through GameManager.instance.myWait.
public WaitForSeconds myWait = new WaitForSeconds(1f);

// Coroutines throughout your project you can call
yield return GameManager.instance.myWait;
// To have the coroutine wait one second.
```
* This will cut down on memory and computation of having multiple parallel "WaitFor's", helping optimization.
* Caching these yields works with `WaitForSeconds(float)`, `WaitForFixedUpdate()` (which waits for the Physics loop Fixed frame), and `WaitForNextFrame()` (which waits for the next normal `Update()` frame).

## Enumerators

Forget what we said about coroutines, Enums are going to be your new **bester** friends.

They're essentially just numbers with names, which means you can make checks more clear and easy to understand. *Computationally they're just integers* (very light), but to your eyes they have nice word-names! (Wow!)

This means in the future you can avoid checking if an object exists on a layer with `LayerMask.NameToLayer("GrossString")`. This fucking method compares a complex data type with no regard for our performance. Don't use strings for IDing things ever again! use Enums instead! They're just integers! But they're kinda not!

Here's an example of a perfect utilization - keeping track of the indices of your layers.

Let's start with a BAD piece of code. I've commented the badness so you know how bad it is.

```c#
if (gameObject.layer == 10) // What is this???!!!! Might've been clear when you wrote it, but not after 3 months.
{
    // Do something but terribly.
}
```
Yikes. So I'm glad we're done with that code. I don't know what that 10 is supposed to be. That could be any layer, and honestly I'm too lazy to check the Layer list in Unity.

Let's use our **enumerator** for this next bit. First let's define it:

```c#
public enum Layer
{
    Default = 0,
    UI = 5,
    Projectile = 8,
    Enemies = 9,
    Environment = 10,
    Gun = 12
}
```
And now instead of that BAD chunk of code, we make this GOOD chunk of code.

```c#
if (gameObject.layer == (int)Layer.Environment) // Oh, it's the Environment layer. Remember to cast to int! (Visual Studio will remind you.)
{
    // Do something but sexy.
}
```

It also has the added bonus that if your layer indexes get shifted, you only have to modify the Enumerator's definitions, and not every occurance throughout the project. Yay! You can even rename a given layer to something else and the index will stay the same. *If you did this using strings you'd have to change every occurance of the string. (!)*

## Worthwhile Resources

* [Polymorphism](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)  
* [Delegates](https://unity3d.com/learn/tutorials/topics/scripting/delegates)  
* [Asynchronus tasks + Coroutines](https://docs.unity3d.com/Manual/Coroutines.html)
