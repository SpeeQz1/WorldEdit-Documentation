## Expression Variables
The following variables can be used in command expressions:

- `t`: tile ID
- `w`: wall ID
- `x`, y: coordinates
- `i`: tile frame X
- `j`: tile frame Y
- `l`: liquid type (0: none, 1: water, 2: lava, 3: honey)
- `p`: paint color
- `pw`: wall paint color
- `s`: slope type
- `h`: half block (true/false)
- `a`: actuator (true/false)
- `in`: inactive (true/false)
- `r1`, `r2`, `r3`, `r4`: wire colors (true/false for red, blue, green, yellow respectively)
- `rand`: random number between 0 and 1

## Selection Commands
//all - Sets the selection to the entire world <br />
//point1 [x] [y] - Sets the first point of the selection <br />
//point2 [x] [y] - Sets the second point of the selection <br />
//select <type> - Sets the selection function (e.g., cuboid, sphere) <br />
//region [name] - Selects a region as a worldedit selection <br />
//near <radius> - Sets the selection to a radius around you <br />
//shift <direction> <amount> - Shifts the selection <br />
//resize <direction(s)> <amount> - Resizes the selection <br />

Expressions are not used in these commands.

Example:
```
//point1 100 100
//point2 200 200
//select cuboid
//resize u 10
```

## Clipboard Operations
//copy - Copies the selection to the clipboard <br />
//cut - Copies the selection to the clipboard, then deletes it <br />
//paste [alignment] [-f] [=> expr] - Pastes the clipboard to the selection <br />
//flip <direction> - Flips the clipboard <br />
//rotate <angle> - Rotates the clipboard <br />
//scale <+/-> <amount> - Scales the clipboard <br />

Expressions in //paste allow conditional pasting based on existing blocks.

Example:
```
//copy
//rotate 90
//paste align=topleft => t == 0
```

## Block Manipulation
//set <tile> [=> expr] - Sets tiles in the selection <br />
//setwall <wall> [=> expr] - Sets walls in the selection <br />
//replace <from> <to> [=> expr] - Replaces tiles in the selection <br />
//replacewall <from> <to> [=> expr] - Replaces walls in the selection <br />
//fill <tile> [=> expr] - Fills the selection with the specified tile <br />
//fillwall <wall> [=> expr] - Fills the selection with the specified wall <br />

Expressions allow conditional execution based on existing blocks.

Example:
```
//set stone => t == 0
//replace dirt stone => t != 0
//fillwall wood => w == 0
```

## Biome and Environment
//biome <biome1> <biome2> - Converts biomes in the selection <br />
//flood <liquid> - Floods liquids in the selection <br />
//drain - Drains liquids in the selection <br />
//mow - Mows grass, thorns, and vines in the selection <br />
//fixgrass - Fixes suffocated grass in the selection <br />

Expressions are not used in these commands.

Example:
```
//biome forest corruption
//flood water
//mow
```

## Aesthetic Modifications
//paint <color> [=> expr] - Paints tiles in the selection <br />
//paintwall <color> [=> expr] - Paints walls in the selection <br />
//slope <type> [=> expr] - Slopes tiles in the selection <br />
//slopedelete [type] [=> expr] - Removes slopes in the selection <br />
//smooth [=> expr] - Smooths blocks in the selection <br />
//outline <tile> <color> <state> [=> expr] - Sets block outline around blocks <br />
//outlinewall <wall> [color] [=> expr] - Sets wall outline around walls <br />

Expressions allow conditional application based on existing blocks or positions.

Example:
```
//paint red => t != 0
//slope halfbrick => y % 2 == 0
//smooth => t == 1 || t == 2
```

## Advanced Shaping
//shape <shape> [rotate] [flip] <tile/wall> [=> expr] - Draws shapes in the selection <br />
//text <text> - Creates text with alphabet statues in the selection <br />

Expressions in //shape allow conditional shape drawing.

Example:
```
//shape circle stone => t == 0
//text Hello World
```

## Wire and Mechanism
//actuator <on/off> [=> expr] - Sets actuators in the selection <br />
//setwire <wire> <state> [=> expr] - Sets wires in the selection <br /> 
//inactive <status> [=> expr] - Sets the inactive status in the selection <br />

Expressions allow conditional application of mechanisms.

Example:
```
//actuator on => t != 0
//setwire 1 on => t == 1 || t == 2
```

## Fixes and Cleanup
//fixghosts - Fixes invisible signs, chests and item frames <br />
//fixhalves - Fixes half blocks in the selection <br />
//fixslopes - Fixes covered slopes in the selection <br />
//killempty <type> - Deletes empty signs and/or chests <br />

Expressions are not used in these commands.

Example:
```
//fixghosts
//killempty all
```

## Schematic Operations
//schematic <subcommand> - Manages worldedit schematics (save, load, delete, list) <br />
//size <clipboard/schematic> [name] - Shows size of clipboard or schematic <br />

Expressions are not used in these commands.

Example:
```
//schematic save myhouse
//schematic load myhouse
//size schematic myhouse
```

## History Management
//undo [steps] [account] - Undoes worldedit actions <br />
//redo [steps] [account] - Redoes worldedit actions <br />

Expressions are not used in these commands.

Example:
```
//undo 5
//redo 3
```

## Special Selection
//magicwand [<X> <Y>] => expr - Creates selection from contiguous tiles matching expression <br />

The expression defines which blocks to include in the selection.

Example:
```
//magicwand => t == 1 || t == 2
```
