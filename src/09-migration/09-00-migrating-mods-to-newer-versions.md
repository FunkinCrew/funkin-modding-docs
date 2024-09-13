# Creating a Friday Night Funkin' Mod - Migrating Mods to Newer Versions

Occasionally, in order to make improvements to the modding system for Friday Night Funkin', the team has to make breaking changes to features that older mods were using, causing them to have unexpected beahavior or otherwise no longer function properly. When we do this, we update the API version rule, automatically flagging any older mods and preventing them from being loaded to ensure the stability of the game.

This chapter will walk you through the process of making older mods compatible with newer versions of Friday Night Funkin'. Once you compete the steps in this guide, your mod should function as expected on newer versions.
