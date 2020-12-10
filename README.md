# Painterly Pack Fan Continuation
## Customizer Source Repo

This repository contains all the available textures and options for customizer for the fan continuation of the painterly pack. To contribute to this project you'll need to add changes in the form of Pull Requests. 

If you're unfamiliar with this process, read our handy guide here: 
[Making Pull Requests the Easy Way](https://github.com/t3rminus/painterly-continuation/blob/main/docs/HOWTO.md)

---

## Contributing
To contribute, fork this repository, add your files, and create a pull-request with your various textures, and option description JSON files. An example with two options for dirt and sand might include the following files:
```
/textures/blocks/dirt:
- dirt-myname.png
- dirt-myname.json
/textures/blocks/sand:
- sand-myname.png
- sand-myname.json
```

The contents of the json are formatted as follows:
```js
{
  "category": "basic", // Select a category
  "name": "Normal Dirt", // Name of your texture
  "choice": "I would like normal dirt in basic beige", // Fun text describing your choice
  "author": "My Name <mycontact@example.com>", // Your name/handle/email/etc.
  "date": "YYYY-MM-DD", // The date you created the texture

  // Optional. Array of editors that contributed, and the date of edit
  "edits": [
    { "author": "Editor Name <editorcontact@example.com", "date": "YYYY-MM-DD" }
  ],

  // Optional. Which file to use as preview (if not specified, will use first output)
  "preview": "dirt-myname.png",

  // List of output files
  "output": {
    "assets/minecraft/textures/block/dirt.png": "dirt-myname.png"
  }
}
```

---

## Categories
Categories roughly map to categories on the original customizer, but with more biome-specific categorization. These may be subject to change as the pack grows. For now, possible categories include:
- basic - dirt, grass block, water, lava, etc
- decorative - wool, cement, terracotta, etc
- vegetation - flowers, mushrooms, growing grass, etc
- wood - leaves, logs, planks, etc
- stone - natural, brick, etc
- ore - natural, smelted blocks, etc
- ice - snow, ice, etc
- ocean - coral, kelp
- desert - sand, sandstone
- cave - dark stone, moss, dripstone
- nether - netheraack, blackstone, basalt, nylium, etc
- end - end stone, purpur, chorus plant
- tools - tools, records, maps, buckets
- armor
- food
- paintings
- dyes
- animals
- hostile
- villagers - friendly, illagers, witches
- effects - particles, weather
- gui
- misc - for pack-related options (icons)

---

## Output Files
One selected option can produce multiple output files. For example, grass is made up of `grass_block_top.png`, `grass_block_side.png`, and `grass_block_side_overlay.png`. Additionally, each output file can be composed of multiple input files (including other output files). The ouput is in the format `"/result/path/in/pack.png": <source(s)>`, where sources is one or more paths to images.

There are four options possible for sources:
- a single file in the same directory as the json
- a file in the output directory, prefixed with `@`
- `_blank` to generate a blank image
- an array of the above options

If an array is specified, the image is composed from left-to-right, with the second entry overlayed on the first, and the third overlayed on top of that, etc.

### Here are some examples:

Single File
```js
"output": {
  "assets/minecraft/textures/block/dirt.png": "dirt-myname.png"
}
```

Composed Image
```js
"output": {
  "assets/minecraft/textures/block/dirt.png": ["dirt1.png", "dirt2.png"]
}
```

Composed Image (based on user's other selection, from the pack-in-progress)
```js
"output": {
  "assets/minecraft/textures/block/coarse_dirt.png":
    ["@assets/minecraft/textures/block/dirt.png", "pebbles.png"]
}
```

Blank Image
```js
"output": {
  "assets/minecraft/textures/misc/underwater.png": "_blank"
}
```

Multiple Output Files
```js
"output": {
  "assets/minecraft/textures/block/grass_block_side.png":
    ["@assets/minecraft/textures/block/dirt.png", "dirt-side.png"],
  "assets/minecraft/textures/block/grass_block_side_overlay.png": "dirt-side.png",
  "assets/minecraft/textures/block/grass_block_top.png": "dirt-top.png"
}
```

---

#### A note on composed images:
While there is nothing technically preventing you from basing a composed image upon another composed image, it is recommended to avoid this. The order that the options are added to the pack is arbitrary, and the composer will simply ignore source files that haven't been composed yet.

However, it is perfectly safe to base a composed image on another image with a single source. Single-source images are copied first, then composed images are generated, so single-source images will always exist in the pack before the composed images are generated.
