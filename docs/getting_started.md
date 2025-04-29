# Getting Started with SpriteAI

SpriteAI is a powerful library for generating game assets using AI. This guide will help you get started with installing and using SpriteAI in your projects.

## Installation

To install SpriteAI, you'll need Node.js and npm installed on your system. Once you have those, you can install SpriteAI using npm:

```bash
npm install spriteai
```

## Basic Usage

### Importing SpriteAI

To use SpriteAI in your project, import the necessary functions:

```javascript
import { generateCharacterSpritesheet, generateLandscapeSprite } from 'spriteai';
```

### Generating a Character Spritesheet

To generate a character spritesheet, use the `generateCharacterSpritesheet` function:

```javascript
const characterDescription = "a brave knight in shining armor";
const options = {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art'
};

const result = await generateCharacterSpritesheet(characterDescription, options);

console.log(result.spritesheet); // Base64 encoded spritesheet
console.log(result.metadata); // Metadata about the generated spritesheet
```

### Generating a Landscape Sprite

To generate a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
const landscapeDescription = "a lush forest with a winding river";
const options = {
  size: '1024x1024',
  style: 'pixel-art',
  timeOfDay: 'day',
  weather: 'clear',
  perspective: 'side-scrolling'
};

const result = await generateLandscapeSprite(landscapeDescription, options);

console.log(result.landscape); // Base64 encoded landscape sprite
console.log(result.metadata); // Metadata about the generated landscape
```

## Main Features

SpriteAI offers several key features for game asset generation:

1. **Character Spritesheets**: Generate animated character spritesheets with customizable states, frames, and styles.
2. **Landscape Sprites**: Create detailed landscape sprites with various environmental settings and perspectives.
3. **Customization Options**: Adjust parameters like size, style, time of day, weather, and more to fine-tune your generated assets.
4. **Metadata**: Receive detailed metadata about your generated assets, including dimensions, frame data, and more.
5. **Background Removal**: Option to remove backgrounds from generated sprites for easier integration into your games.

## Advanced Usage

### Fetching Available Animation States

You can fetch the available animation states for character spritesheets:

```javascript
import { fetchAvailableAnimationStates } from 'spriteai';

const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### Fetching Available Sprite Styles

To get a list of available sprite styles:

```javascript
import { fetchAvailableSpriteStyles } from 'spriteai';

const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

### Generating Environment Sprites

For creating tileset-style environment sprites:

```javascript
import { generateEnvironmentSprites } from 'spriteai';

const description = "medieval castle";
const options = {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  theme: 'fantasy'
};

const result = await generateEnvironmentSprites(description, options);
console.log(result.tileset); // Base64 encoded tileset
console.log(result.metadata); // Metadata about the generated tileset
```

### Generating Item Sprites

To create a collection of item sprites:

```javascript
import { generateItemSprites } from 'spriteai';

const description = "magical artifacts";
const options = {
  itemCount: 4,
  size: '1024x1024',
  style: 'pixel-art',
  itemType: 'equipment'
};

const result = await generateItemSprites(description, options);
console.log(result.itemSheet); // Base64 encoded item sheet
console.log(result.metadata); // Metadata about the generated items
```

## Conclusion

This guide covers the basics of using SpriteAI to generate game assets. Explore the various functions and options to create unique and customized sprites for your game projects. For more detailed information on each function and its parameters, refer to the API documentation.