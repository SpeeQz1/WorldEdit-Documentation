Here is an updated version of the WorldEdit documentation, incorporating corrections and additions based on the provided source code:

# WorldEdit Documentation

## Expression Variables
The following variables can be used in command expressions:

- `t`, `tile`: tile is active (true/false)
- `nt`, `ntile`: tile is not active (true/false)
- `w`, `wall`: wall ID (0 for no wall)
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
//point1 [x] [y] - Sets the first point of the selection <br />
//point2 [x] [y] - Sets the second point of the selection <br />
//select <type> - Sets the selection function (e.g., normal, altcheckers, checkers, ellipse, border, outline) <br />
//region [name] - Selects a region as a worldedit selection <br />
//near <radius> - Sets the selection to a radius around you <br />
//shift <direction> <amount> - Shifts the selection <br />
//resize <direction(s)> <amount> - Resizes the selection <br />
//magicwand [<X> <Y>] => expr - Creates selection from contiguous tiles matching expression <br />

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
//copy - Copies the selection to the clipboard <br />
//cut - Copies the selection to the clipboard, then deletes it <br />
//paste [alignment] [-f] [=> expr] - Pastes the clipboard to the selection <br />
//spaste [alignment] [-flag -flag ...] [=> expr] - Pastes the clipboard with specific conditions <br />
//flip <direction> - Flips the clipboard <br />
//rotate <angle> - Rotates the clipboard <br />
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
//setwall <wall> [=> expr] - Sets walls in the selection <br />
//replace <from> <to> [=> expr] - Replaces tiles in the selection <br />
//replacewall <from> <to> [=> expr] - Replaces walls in the selection <br />
//fill <tile> [=> expr] - Fills the selection with the specified tile <br />
//fillwall <wall> [=> expr] - Fills the selection with the specified wall <br />
//coat [-]<echo|illuminant|none> [=> expr] - Coats tiles in the selection <br />
//coatwalls [-]<echo|illuminant|none> [=> expr] - Coats walls in the selection <br />

Expressions allow conditional execution based on existing blocks.

Example:
```
//set stone => t == 0
//replace dirt stone => t != 0
//fillwall wood => w == 0
//coat echo => t != 0
```

## Biome and Environment
//biome <biome1> <biome2> - Converts biomes in the selection <br />
//flood <liquid> - Floods liquids in the selection <br />
//drain - Drains liquids in the selection <br />
//mow - Mows grass, thorns, and vines in the selection <br />
//fixgrass - Fixes suffocated grass in the selection <br />
//setgrass <grass> [=> expr] - Sets certain grass in the selection <br />

Expressions are used in the //setgrass command.

Example:
```
//biome forest corruption
//flood water
//mow
//setgrass jungle => t == 0
```

## Aesthetic Modifications
//paint <color> [=> expr] - Paints tiles in the selection <br />
//paintwall <color> [=> expr] - Paints walls in the selection <br />
//slope <type> [=> expr] - Slopes tiles in the selection <br />
//delslope [type] [=> expr] - Removes slopes in the selection <br />
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
//shapefill <shape> [rotate] [flip] <tile/wall> [=> expr] - Draws filled shapes in the selection <br />
//shapewall <shape> [rotate] [flip] <wall> [=> expr] - Draws shapes with walls in the selection <br />
//shapewallfill <shape> [rotate] [flip] <wall> [=> expr] - Draws filled shapes with walls in the selection <br />
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
//killempty <signs/chests/all> - Deletes empty signs and/or chests <br />

Expressions are not used in these commands.

Example:
```
//fixghosts
//killempty all
```

## Schematic Operations
//schematic <subcommand> - Manages worldedit schematics (save, load, delete, list, copysave, paste) <br />
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

## Miscellaneous
//move <right> <down> [=> expr] - Moves tiles from the selection to new area <br />
//activate <sign/chest/itemframe/sensor/dummy/weaponrack/pylon/mannequin/hatrack/foodplate/all> - Activates non-working objects <br />

Expressions can be used in the //move command.

Example:
```
//move 10 5 => t != 0
//activate all
```

This updated documentation includes corrections, additional commands, and more accurate descriptions based on the provided source code.
