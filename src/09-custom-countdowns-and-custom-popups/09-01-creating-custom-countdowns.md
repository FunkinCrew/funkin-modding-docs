# Creating Custom Countdowns

All custom countdowns are based on the [current note style](../08-custom-notestyles/08-00-custom-notestyles.md) that is being used in-game. With that being said, you have to [add your assets](../01-fundamentals/01-03-asset-replacement-and-additions.md#asset-replacement-and-additons) with the note style name you are going to use.

You can add both graphic as well sound assets you are going to use for your countdown:
- The PNG files need to go into `images/countdown/<notestyleid>`, replacing the `<notestyleid>` with the internal name of our notestyle
- The OGG files need to go into `shared/sounds/gameplay/countdown/<notestyleid>`, again replacing `<notestyleid>` with the internal name of our notestyle.

We'll end up with something like this.

```
-mods
 |-myMod
   |-images
     |-countdown
       |-myNotestyle
         |-ready.png
         |-set.png
         |-go.png
   |-shared
     |-sounds
       |-gameplay
         |-countdown
           |-myNotestyle
             |-introTHREE.ogg
             |-introTWO.ogg
             |-introONE.ogg
             |-introGO.ogg
   |-_polymod_metadata.json
```