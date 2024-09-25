# WorldEdit Documentation

## Expression Variables
The following variables can be used in command expressions:

- `t`, `tile`: <br />
&emsp;tile ID (0 for no tile) <br />
&emsp;checks if it is a tile (true/false) 
- `nt`, `ntile`: checks if it is not a tile (true/false)
- `w`, `wall`: <br />
&emsp;wall ID (0 for no wall) <br />
&emsp;checks if it is a wall (true/false)
- `nw`, `nwall`: no wall (true/false)
- `x`, `y`: coordinates
- `lh`, `honey`, `nlh`, `nhoney`: liquid is honey (true/false)
- `ll`, `lava`, `nll`, `nlava`: liquid is lava (true/false)
- `lw`, `water`, `nlw`, `nwater`: liquid is water (true/false)
- `li`, `liquid`, `nli`, `nliquid`: liquid present/not present (true/false)
- `tp`, `tilepaint`, `ntp`, `ntilepaint`: tile paint color (0 for no paint)
- `wp`, `wallpaint`, `nwp`, `nwallpaint`: wall paint color (0 for no paint)
- `s`, `slope`, `ns`, `nslope`: slope type
- `wire`, `wire1`, `wirered`, `redwire`: red wire (true/false)
- `wire2`, `wireblue`, `bluewire`: blue wire (true/false)
- `wire3`, `wiregreen`, `greenwire`: green wire (true/false)
- `wire4`, `wireyellow`, `yellowwire`: yellow wire (true/false)
- `nwire`, `nwire1`, `nwirered`, `nredwire`: no red wire (true/false)
- `nwire2`, `nwireblue`, `nbluewire`: no blue wire (true/false)
- `nwire3`, `nwiregreen`, `ngreenwire`: no green wire (true/false)
- `nwire4`, `nwireyellow`, `nyellowwire`: no yellow wire (true/false)
- `a`, `active`, `na`, `nactive`: tile active/inactive state
- `ac`, `actuator`, `nac`, `nactuator`: actuator present/not present (true/false)

## Selection Commands
//all - Sets the selection to the entire world <br />
//point1, //p1 [x] [y] - Sets the first point of the selection <br />
//point2, //p2 [x] [y] - Sets the second point of the selection <br />
//select <type> - Sets the selection function (types: normal, altcheckers, checkers, ellipse, border, outline) <br />
//region [name] - Selects a region as a worldedit selection <br />
//near <radius> - Sets the selection to a radius around you <br />
//shift <direction> <amount> - Shifts the selection (directions: u, d, l, r) <br />
//resize <direction(s)> <amount> - Resizes the selection (directions: u, d, l, r) <br />
//magicwand, //mwand, //mw [<X> <Y>] => expr - Creates selection from contiguous tiles matching expression <br />

Expressions are not used in most of these commands, except for //magicwand.

Example:
```
//point1 100 100
//point2 200 200
//select normal
//resize u 10
//magicwand => t == 1 || t == 2
```

## Clipboard Operations
//copy, //c - Copies the selection to the clipboard <br />
//cut - Copies the selection to the clipboard, then deletes it <br />
//paste, //p [alignment] [-f] [=> expr] - Pastes the clipboard to the selection (alignments: l, r, t, b) <br />
//spaste, //sp [alignment] [-flag -flag ...] [=> expr] - Pastes the clipboard with specific conditions (flags: -t, -tp, -et, -w, -wp, -wi, -l) <br />
//flip <direction> - Flips the clipboard (directions: x, y) <br />
//rotate <angle> - Rotates the clipboard (angles: 90, 180, 270) <br />
//scale <+/-> <amount> - Scales the clipboard <br />

Expressions in //paste and //spaste allow conditional pasting based on existing blocks.

Example:
```
//copy
//rotate 90
//paste align=topleft => t == 0
//spaste -t -wp => w != 0
```

## Block Manipulation
//set <tile> [=> expr] - Sets tiles in the selection <br />
//setwall, //swa <wall> [=> expr] - Sets walls in the selection <br />
//replace, //rep <from> <to> [=> expr] - Replaces tiles in the selection <br />
//replacewall, //repw <from> <to> [=> expr] - Replaces walls in the selection <br />
//fill <tile> [=> expr] - Fills the selection with the specified tile <br />
//fillwall, //fillw <wall> [=> expr] - Fills the selection with the specified wall <br />
//coat, //co [-]<echo|e|illuminant|i|none|n> [=> expr] - Coats tiles in the selection <br />
//coatwalls, //coatwall, //cw [-]<echo|e|illuminant|i|none|n> [=> expr] - Coats walls in the selection <br />

Expressions allow conditional execution based on existing blocks.

Example:
```
//set stone => t == 0
//replace dirt stone => t != 0
//fillwall wood => w == 0
//coat echo => t != 0
```

## Biome and Environment
//biome <biome1> <biome2> - Converts biomes in the selection (biomes: forest, corruption, crimson, hallow, jungle, mushroom, snow, desert, ocean, hell) <br />
//flood <liquid> - Floods liquids in the selection (liquids: water, lava, honey) <br />
//drain - Drains liquids in the selection <br />
//mow - Mows grass, thorns, and vines in the selection <br />
//fixgrass - Fixes suffocated grass in the selection <br />
//setgrass <grass> [=> expr] - Sets certain grass in the selection (grass types: forest, corruption, crimson, hallow, jungle, mushroom) <br />

Expressions are used in the //setgrass command.

Example:
```
//biome forest corruption
//flood water
//mow
//setgrass jungle => t == 0
```

## Aesthetic Modifications
//paint, //pa <color> [=> expr] - Paints tiles in the selection <br />
//paintwall, //paw <color> [=> expr] - Paints walls in the selection <br />
//slope <type> [=> expr] - Slopes tiles in the selection (types: none, t, tr, tl, br, bl) <br />
//delslope, //delslopes, //dslope, //dslopes [type] [=> expr] - Removes slopes in the selection <br />
//smooth [=> expr] - Smooths blocks in the selection <br />
//outline, //ol <tile> <color> <state> [=> expr] - Sets block outline around blocks (states: active, inactive) <br />
//outlinewall, //olw <wall> [color] [=> expr] - Sets wall outline around walls <br />

Expressions allow conditional application based on existing blocks or positions.

Example:
```
//paint red => t != 0
//slope halfbrick => y % 2 == 0
//smooth => t == 1 || t == 2
```

## Advanced Shaping
//shape, //shapefill, //shapef <shape> [rotate] [flip] <tile/wall> [=> expr] - Draws shapes in the selection <br />
//shapewall, //shapew, //shapewallfill, //shapewf <shape> [rotate] [flip] <wall> [=> expr] - Draws shapes with walls in the selection <br />
(Shapes: line/l, rectangle/r, ellipse/e, isoscelestriangle/it, righttriangle/rt) <br />
(Rotate types for triangles: up/u, down/d, left/l, right/r) <br />
(Flip types for right triangles: left/l, right/r) <br />
//text <text> - Creates text with alphabet statues in the selection <br />

Expressions in shape commands allow conditional shape drawing.

Example:
```
//shape circle stone => t == 0
//shapefill rectangle dirt => t != 0
//text Hello World
```

## Wire and Mechanism
//actuator <on/off> [=> expr] - Sets actuators in the selection <br />
//setwire, //swi <wire> <state> [=> expr] - Sets wires in the selection (wires: 1, 2, 3, 4; states: on, off) <br />
//inactive, //ia <status> [=> expr] - Sets the inactive status in the selection (status: on, off, reverse) <br />

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
//killempty <signs/chests/all> - Deletes empty signs and/or chests <br />

Expressions are not used in these commands.

Example:
```
//fixghosts
//killempty all
```

## Schematic Operations
//schematic, //schem, //sc <subcommand> - Manages worldedit schematics <br />
Subcommands: <br />

* delete, del <name> <br />
* list [page] <br />
* load, l <name> <br />
* save, s [-force/-f] <name> <br />
* copysave, cs [-force/-f] <name> <br />
* paste, p [alignment] [-f] [=> expr] - Pastes the clipboard to the selection <br />
(Alignment options: l, r, t, b or any combination like lt, rb. l=left, r=right, t=top, b=bottom)

//size <clipboard/c> [user name] - Shows size of clipboard <br />
//size <schematic/s> <name> - Shows size of schematic <br />

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

## Miscellaneous
//move <right> <down> [=> expr] - Moves tiles from the selection to new area <br />
//activate <type> - Activates non-working objects <br />
(Types: sign/s, chest/c, itemframe/i/frame, sensor/l/logic, dummy/d/targetdummy, weaponrack/w, pylon/p, mannequin/m, hatrack/h, foodplate/f/plate, all/a) <br />

Expressions can be used in the //move command.

Example:
```
//move 10 5 => t != 0
//activate all
```

This updated documentation includes corrections, additional commands, and more accurate descriptions based on the provided source code.
