# Creating a Friday Night Funkin' Mod - Custom Modules

This guide will walk you through the process of creating a functioning, fully compatible Friday Night Funkin' mod, using the game's official systems for loading custom content and scripts. Once your mod is complete, you will be able to place it in the `mods` folder in your game install and use its content in-game without overriding the base game content and still maintain compatibility with other mods.

This entry goes over making custom modules for your mod

## what are modules?
modules are scripts that allow you to interact with the full game with only functions/callbacks, you can use them to alter ui elements in menus, and edit the game feild in the song without having to make a script for the stage/song/character

## how modules work
modules are taken care of by the ModuleHandler in the game that takes every class that extends `funkin.modding.module.Module` and handles it by firing its callbacks

## where to add the module file
first you need to make a scripts folder if you dont already have one in your mods folder. for where you should add your module file(s) in that folder it doesnt really matter, you can add them in folders to keep your files clean so the next part is optional, make a folder called `modules` in `yourmod/scripts/.`. and then make a file named `yourModule.hxc` in that folder, you dont have to make the first letter upperCase like hx files and offcourse change 'yourModule' to your modules name

## how to make a module
to make a module you need some scripting knowledge so you can understand how it works, so in that file that you created make a class with the name of your module (make sure the first letter is uppercase) and make it extend `funkin.modding.module.Module` after that override the classes constructor and in the super call function add the classes name in a string

```
import funkin.modding.module.Module;

class MyModule extends Module{
  override public function new()
  {
    super('MyModule'); // <-- your modules name here
  }
}
```

## how to add callbacks to a module

--add something here

