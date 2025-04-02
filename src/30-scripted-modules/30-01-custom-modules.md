# Creating a Friday Night Funkin' Mod - Custom Modules

This guide will walk you through the process of creating a functioning, fully compatible Friday Night Funkin' mod, using the game's official systems for loading custom content and scripts. Once your mod is complete, you will be able to place it in the `mods` folder in your game install and use its content in-game without overriding the base game content and still maintain compatibility with other mods.

This entry goes over making custom script modules for your mod.

## What are modules?

Modules are singleton, "global" script classes that allow you to do... really anything! They can be used to inject something into a state, to modify parts of gameplay like the HUD, to add systems and helpers for mods to use, to add entirely new features to the game, whatever you want! Within the limits of Hscript and Polymod, of course.

## How modules work

Each module is initialized with a unique `id` string that is used to identify it, as well as a `priority` integer that collectively determine the order they are all loaded in, as well as the order their callbacks are called in. The greater the number, the later it's processed (alphabetical by ID if the priorities are the same). The number can be any integer, even negative, and defaults to 1000 if none provided. It's a very helpful feature to utilize in case any modules depend on another!

`ModuleHandler` is the class that handles all module instances internally, but it's also to be used by scripts to get the module instances to interact with via `ModuleHandler.getModule(id:String):Module`.

## Example

In a script `mymod/scripts/mymod/mysubpackage/Example.hxc`:

```haxe
package mymod.mysubpackage;

import funkin.modding.module.Module; // or use ScriptedModule, it doesn't matter
import funkin.modding.module.ModuleHandler;

class MyModule1 extends Module {
  override public function new() {
    super("mymod-MyModule1", 0); // <-- your module id and priority respectively
  }
  
  override public function onCreate(event:ScriptEvent):Void {
    trace("Hello from mymod-MyModule1!");
  }
  
  public var someVar:Int = 69;
  
  public function someFunction(someArg1:Float, someArg2:Bool = true):Void {
    trace("someArg1: " + Std.string(someArg1));
    trace("someArg2: " + Std.string(someArg2));
  }
}

class MyModule2 extends Module {
  override public function new() {
    super("mymod-MyModule2", 1);
  }
  
  override public function onCreate(event:ScriptEvent):Void {
    trace("Hello from mymod-MyModule2!");
    
    var myModule1:Module = ModuleHandler.getModule("mymod-MyModule1");
    myModule1.scriptCall("someFunction", [myModule1.scriptGet("someVar")]);
  }
}
```

The output from this example should show something like:

```
Hello from mymod-MyModule1!
Hello from mymod-MyModule2!
someArg1: 69
someArg2: true
```

## Some advice

Module IDs must be unique to avoid conflicts with other mods; therefore, it's recommended as a good practice to prefix your module IDs with with your mod name like `mymod-MyModule` or the package of the script like `mymod.mysubpackage.MyModule`. Just anything that'll make it unique! It'll be pretty wordy... but the tradeoff for stability is often worth it.
