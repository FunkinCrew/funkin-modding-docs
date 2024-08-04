# Creating Custom Popups

All custom popups are based on the [current note style](../08-custom-notestyles/08-00-custom-notestyles.md) that is being used in-game. With that being said, you have to [add your assets](../01-fundamentals/01-03-asset-replacement-and-additions.md) with the note style name you are going to use.

You can ONLY add graphic assets you are going to use for your countdown:
- The PNG files need to go into `images/ui/<notestyleid>`, replacing the `<notestyleid>` with the internal name of our notestyle

We'll end up with something like this.

```
-mods
 |-myMod
   |-images
     |-ui
       |-myNotestyle
         |-num0.png
         |-num1.png
         |-num2.png
         |-num3.png
         |-num4.png
         |-num5.png
         |-num6.png
         |-num7.png
         |-num8.png
         |-num9.png
         |-combo.png
         |-sick.png
         |-good.png
         |-bad.png
         |-shit.png
   |-_polymod_metadata.json
```