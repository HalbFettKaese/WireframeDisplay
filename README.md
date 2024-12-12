# WireframeDisplay
 A small resource pack that makes it easy to create and display wireframes of any size that look like those in vanilla.

![2024-09-29_00 41 54](https://github.com/user-attachments/assets/c8f58cc7-d075-4c84-8fa7-8e612ae91fd5)

## Spawning a wireframe display
 The wireframe displays are just item models. You can spawn them as a display like this:

 ```
 # Spawn white wireframe (like from F3 + B):
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:item_model":"wireframe:wireframe_white"}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}

 # Spawn wireframe that is tinted red using custom model data:
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:item_model":"wireframe:wireframe_white",custom_model_data:{colors:[[1,0,0]]}}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}
 
 # Spawn thick white wireframe
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:item_model":"wireframe:wireframe_white_thick"}} ,transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}
 
 # Spawn black wireframe (like the block selection outline)
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:item_model":"wireframe:wireframe_black"}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}
 ```

## Creating more wireframe types
 The pack makes it very easy to add more types of wireframes. You can look at the existing types to get examples, but when you want to make your own, you just have to follow these steps:
 1. Create a new texture. For this, just copy one of the existing textures and rename it.
 2. Edit the wireframe color. The color is written into the 2x3 area to the right of the marker pixels in the top left corner. (DO NOT CHANGE THE MARKER PIXELS THAT ARE IN THE CORNER)
 3. Edit the wireframe thickness. (default: 2.5 pixels) The thickness is written into the 2x3 area to the right of the color pixels. A number x is encoded as a color by first [converting it to a hexadecimal](https://www.rapidtables.com/convert/number/decimal-to-hex.html), which, for example, converts `4.625` in decimal to `4.A` in hexadecimal. Then you take the first two digits before the `.` and the first four digits after the `.` and combine them into one hex code, in this example `#04A000`. You just fill the 2x3 thickness pixels to use this color, and it will use your original `x` as the line thickness. If you don't want to change the thickness, just keep those pixels transparent.
 4. Create a new model of the following format:
 ```json
 {
    "parent": "wireframe:item/wireframe_template",
    "textures": {
        "0": "<path to your new texture>"
    }
 }
 ```

 All that's left is to put your item model on a display entity, and that's it.

 When changing the color or the thickness, you can also choose between editing the first, second or third row to only change the properties of lines along the x, y or z axis.

## Creating more wireframe shapes
### Different cuboid sizes
 You don't need to edit anything about the resource pack if you want to change the size of a given wireframe. Just change the `transformation.scale` of the display entity that the wireframe is on, and adjust the translation.

### Rotating wireframes
 You can use any horizontal rotation, but sadly, any rotation outside of that axis (such as pitch or roll) does not work for the wireframes.

### More complicated shapes
 Let's say you want to make a hammer that breaks 3x3 blocks at once, and so you want to add a 3x3 cluster of block outlines. It would be possible to just spawn 9 separate markers, but that causes issues with multiple transparent outlines overlapping to create a more intense color.

 This can be worked around by creating one single 3x3 model that follows the example of the `wireframe:item/wireframe_template` model. In this, any element in the x-direction should use the `faces` from that model's first 4 elements, any element in the y-direction should use the `faces` from that model's middle 4 elements, and any element in the z-direction should use the `faces` from that example model's last 4 elements.

 With this, you can add the 32 edges that a 3x3x1 wireframe of cubes needs to a single model, and set the `faces` of each element according to the example of the given template model.

 An alternative to making one single 3x3 model in this example would be to create variations of the standard template that have missing edges, so you can combine multiple of these to create a shape with no duplicate edges.

 Yet another alternative would be to just make one single 3x3x1 box.

## In earlier versions
 The pack is designed to work for 1.21.2, but has overlays that let it work in earlier versions. For this, the standard item models are also defined as different `custom_model_data` variants of `coal` items. So in 1.21.1, you can use these commands instead:

 ```
 # Spawn white wireframe (like from F3 + B):
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:custom_model_data":1}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}

 # Spawn thick white wireframe
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:custom_model_data":2}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}

 # Spawn black wireframe (like the block selection outline)
 /execute align xyz run summon item_display ~ ~ ~ {item: {id:"coal",components: {"minecraft:custom_model_data":3}}, transformation:{scale:[1f,1f,1f],left_rotation:[0f,0f,0f, 1f],right_rotation:[0f,0f,0f,1f],translation:[0.5,0.5,0.5]}}
 ```

## Credits
 All of the contents of this resource pack were written by me, but the original problem statement as well as some suggestions for debugging have been provided by [Mqxx](https://github.com/Mqxx). Also thanks to Discord user merak48763 for suggesting a better format to encode the line width.

If you want to thank me for my work, please consider making a small donation.\
[![Donate](https://img.shields.io/badge/Donate-Ko--fi-green.svg)](https://ko-fi.com/halbfettkaese)
