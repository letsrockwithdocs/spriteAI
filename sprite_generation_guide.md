# Sprite Generation Guide

This guide will walk you through the process of using SpriteAI to generate various types of sprites for your game development needs. SpriteAI offers powerful functions to create character spritesheets, landscape sprites, and item sprites with customizable options.

## Table of Contents

1. [Generating Character Spritesheets](#generating-character-spritesheets)
2. [Creating Landscape Sprites](#creating-landscape-sprites)
3. [Producing Item Sprites](#producing-item-sprites)
4. [Additional Utility Functions](#additional-utility-functions)

## Generating Character Spritesheets

The `generateCharacterSpritesheet` function allows you to create detailed character spritesheets with various animation states.

### Basic Usage

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const result = await generateCharacterSpritesheet('a medieval knight in armor');
```

### Customization Options

You can customize the spritesheet generation with the following options:

- `states`: Array of animation states (default: `['idle', 'walk', 'run', 'attack']`)
- `framesPerState`: Number of frames for each state (default: `6`)
- `size`: Output size of the spritesheet (default: `'1024x1024'`)
- `style`: Art style of the sprite (default: `'pixel-art'`)
- `padding`: Padding between sprites (default: `1`)
- `direction`: Base direction of the character (default: `'right'`)
- `save`: Boolean to save the generated image (default: `false`)

### Example with Custom Options

```javascript
const knightSpritesheet = await generateCharacterSpritesheet('a medieval knight in armor', {
  states: ['idle', 'walk', 'run', 'attack', 'defend'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'vector',
  direction: 'left',
  save: true
});

console.log(knightSpritesheet.metadata);
```

## Creating Landscape Sprites

The `generateLandscapeSprite` function helps you create detailed landscape sprites for game backgrounds.

### Basic Usage

```javascript
import { generateLandscapeSprite } from 'spriteAI';

const result = await generateLandscapeSprite('a lush forest with a hidden waterfall');
```

### Customization Options

You can customize the landscape sprite generation with the following options:

- `size`: Output size of the sprite (default: `'1024x1024'`)
- `style`: Art style of the sprite (default: `'pixel-art'`)
- `timeOfDay`: Time setting (default: `'day'`, options: `'day'`, `'night'`, `'sunset'`, `'dawn'`)
- `weather`: Weather conditions (default: `'clear'`, options: `'clear'`, `'rainy'`, `'foggy'`, `'snowy'`)
- `perspective`: View perspective (default: `'side-scrolling'`, options: `'side-scrolling'`, `'top-down'`, `'isometric'`)
- `save`: Boolean to save the generated image (default: `false`)
- `removeBackground`: Boolean to remove the background (optional)
- `backgroundColor`: Background color to remove (if `removeBackground` is true)
- `colorThreshold`: Threshold for background color removal (if `removeBackground` is true)

### Example with Custom Options

```javascript
const forestSprite = await generateLandscapeSprite('a lush forest with a hidden waterfall', {
  size: '2048x1024',
  style: 'hand-drawn',
  timeOfDay: 'sunset',
  weather: 'foggy',
  perspective: 'isometric',
  save: true,
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  colorThreshold: 0.1
});

console.log(forestSprite.metadata);
```

## Producing Item Sprites

The `generateItemSprites` function allows you to create collections of item sprites for game inventories or pickups.

### Basic Usage

```javascript
import { generateItemSprites } from 'spriteAI';

const result = await generateItemSprites('magical potions and elixirs');
```

### Customization Options

You can customize the item sprite generation with the following options:

- `itemCount`: Number of items to generate (default: `4`)
- `size`: Output size of the sprite sheet (default: `'1024x1024'`)
- `style`: Art style of the sprites (default: `'pixel-art'`)
- `padding`: Padding between sprites (default: `1`)
- `itemType`: Type of items to generate (default: `'equipment'`)
- `background`: Background color (default: `'white'`)
- `save`: Boolean to save the generated image (default: `false`)

### Example with Custom Options

```javascript
const potionSprites = await generateItemSprites('magical potions and elixirs', {
  itemCount: 6,
  size: '1536x1536',
  style: 'vector',
  itemType: 'consumable',
  background: 'transparent',
  save: true
});

console.log(potionSprites.metadata);
```

## Additional Utility Functions

SpriteAI provides some utility functions to help with sprite generation:

### Fetching Available Animation States

```javascript
import { fetchAvailableAnimationStates } from 'spriteAI';

const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### Fetching Available Sprite Styles

```javascript
import { fetchAvailableSpriteStyles } from 'spriteAI';

const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

These utility functions can be useful when you want to provide options to users or dynamically adjust your sprite generation parameters.

Remember that all generated sprites are returned as base64-encoded strings, which can be easily used in web applications or saved to files. The metadata provided with each result contains valuable information about the generated sprites, including dimensions, frame data, and other relevant details.

Happy sprite generating with SpriteAI!