# **exportmaps**
A DFHack plugin for exporting world maps while in game.

## What does it do?
It exports almost all the world maps (and many more) while you are playing the game (Fortress or Adventure). There's no need to enter Legends mode.

You can also use it in Legends mode, as it provides a very fast way to exports the maps.

The following standard DF maps can be generated:

* Elevations including lake and ocean floors
* Elevation respecting water level
* Biome
* Hydrosphere
* Temperature
* Rainfall
* Drainage
* Savagery
* Volcanism
* Current Vegetation
* Evil
* Salinity
* Structures/fields/roads/etc (disabled in Mac)
* Trade
* Nobility/holdings
* Diplomacy
* Region **(NEW!)**

Only enhanced biome map is not generated, as I consider it confusing and useless.

## Are the exported maps identical to the ones generated by DF?
Yes. Their content is the same as the one generated by DF. The only difference is that
the exported map is generated in .PNG format instead of .BMP to reduce disk space.

Below is a sites/structure map comparison between the map generated by DF and the one generated by the plugin.

![alt tag](https://github.com/ragundo/exportmaps/blob/master/docs/xites.png)
Click in the image and pulse RAW buttom in Github to see in full resolution.

## Is it fast?
Very,very fast. Exportmaps uses a thread for each map to be generated, so it uses all the cores of your computer for generating them.
The world is visited only once, generating the data for each world coordinate. The different threads process that data simultaneously
to generate the maps.

In contrast, DF only allows you to generate them one map each time.

**NOTE:** Sites/Structures/Roads is, by far, the slowest map to generate as a full realization of each world site needs to be
generated, added to the map and destroyed. If you want to speed up the generation, export all the maps except this one.

## New maps
As the plugin gets the data natively from DF, new map types can be generated. The first one is the region map, which shows all the
world regions colored according to its type: OCEAN, TUNDRA, HILL, etc.

![alt tag](https://github.com/ragundo/exportmaps/blob/master/docs/region_maps.png)

A world region can contain several biomes, but they're removed in this map so it looks like a simplification of the biome one.

## Raw maps
Additionally to standard DF image maps, with this plugin you can generate raw maps which are binary files with data extracted directly from DF,
ready to be processed by an external tool.
<a href="docs/raw_maps.md">Read more details about them.</a>

## Height Maps
Heightmaps are raw maps encoded as a grayscale PNG with their values scaled to the range 0-255
(a elevation of 123 is translated to a pixel with color RGB(123,123,123)).

Several DF maps are already exported as heightmaps:

* Temperature
* Rainfall
* Drainage
* Savagery
* Volcanism
* Current Vegetation
* Evil
* Salinity

Unfortunately, the most interesting heightmap types are not generated by DF: elevation and elevation respecting
water levels.

DF generates those maps, but they're not truly heightmaps, as the ocean is blue color coded.

To solve this, and generate a true elevation heightmap, type in the console:

`exportmaps -elevation-hm`

for the elevation heightmap or

`exportmaps -elevation-water-hm`

for the elevation respecting water levels heightmap. Below is a composition of DF's elevation
respecting water map and it's corresponding true heightmap

![alt tag](https://github.com/ragundo/exportmaps/blob/master/docs/heightmaps.png)

You can import this heightmap, for example, in Blender and view it in 3D:

![alt tag](https://github.com/ragundo/exportmaps/blob/master/docs/blender.png)



## Is it multiplatform?
This plugin requires some trickery to get the data natively from DF. As I don't have access to a Mac computer,
a OS X version is provided as is, compilable (I think) but completely unsupported.
The plugin has been tested in Linux and Windows only.


## But there's already a exportlegends script, isn't?
Yes. You can use `exportlegends maps` to generate the maps, but:

* You need to exit your game and enter legends mode
* It only simulates the keypresses needed to tell DF to generate the map. You're single core again.


## How do I use it?
For the impatient, load a game and type in the DFHack console:

`exportmaps -all-df`

This will generate most of the legends mode maps and write them to disk. This is the prefered way to do it as it's more efficient than generating them
one by one.

If you want to generate only a specific map, you can provide the map type that you want using a command line option:

`exportmaps -biome`

will generate only the biome map. You can also chain map types, so

`exportmaps -biome -vegetation`

will generate the biome and the vegetation maps.

The availble options are the following:

| Command | Map generated |
| --- | --- |
| -temperature     | TEMPERATURE |
| -rainfall        | RAINFALL |
| -drainage        | DRAINAGE |
| -savagery        | SAVAGERY |
| -volcanism       | VOLCANISM |
| -vegetation      | VEGETATION |
| -evilness        | EVILNESS |
| -salinity        | SALINITY |
| -hydrosphere     | HYDROSPHERE |
| -elevation       | ELEVATION |
| -elevation-water | ELEVATION RESPECTING WATER |
| -biome           | BIOME |
| -trading         | TRADING |
| -nobility        | NOBILITY AND HOLDINGS |
| -diplomacy       | DIPLOMACY |
| -sites           | SITES / STRUCTURES / ROADS (Not working in Mac)|
| -region          | WORLD REGIONS **(NEW!)** |
| -all-df          | ALL DF STYLE MAPS |
| -all-raw         | ALL RAW STYLE MAPS |
| -all-hm          | ELEVATION AND ELEVATION RESPECTING WATER HEIGHTMAPS |


## What's next?
For next releases, this is what's planned:

#### New map types
More maps are planned, like geology ones.

#### RPC interface
For generating maps on demand without needing to use the DFHack console. Just connect to DF and request a map using Google's protocol buffers.

#### Site exporting
Similar to DF export site. Get a detailed PNG of a world site.

## Support
You can use Github's Issues to get support about the plugin. Also you can contact me in #dfhack on IRC freenode.

## Thanks to
Warmist, Lethosor, Japa, Q, Angavrilov and all the wonderful people of #dfhack in freenode.
Without their support, this plugin will never have been developed!!!.
