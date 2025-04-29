# Getting Started with SpriteAI

Welcome to SpriteAI, a powerful library for generating game assets using AI. This guide will help you get started with installing and using SpriteAI in your projects.

## Installation

To install SpriteAI, you'll need Node.js (version 12 or higher) and npm. Follow these steps to set up the library:

1. Install SpriteAI using npm:

```bash
npm install spriteai
```

2. If you haven't already, you'll need to set up an OpenAI account and obtain an API key. Store this key securely as an environment variable or in a configuration file.

## Basic Usage

Here's a quick example of how to use SpriteAI to generate a character spritesheet:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

async function createCharacter() {
  const result = await generateCharacterSpritesheet('a medieval knight', {
    states: ['idle', 'walk', 'attack'],
    framesPerState: 4,
    style: 'pixel-art'
  });

  console.log('Spritesheet generated:', result.spritesheet);
  console.log('Metadata:', result.metadata);
}

createCharacter();
```

This will generate a pixel-art spritesheet of a medieval knight with idle, walk, and attack animations.

## Main Features

SpriteAI offers several key features for game asset generation:

### 1. Character Spritesheets

Generate complete character spritesheets with multiple animation states using `generateCharacterSpritesheet()`. You can customize:

- Animation states
- Number of frames per state
- Art style
- Output size
- Character direction

### 2. Landscape Sprites

Create game backgrounds and environment pieces with `generateLandscapeSprite()`. Customize:

- Time of day
- Weather conditions
- Perspective (side-scrolling, top-down, isometric)
- Art style

### 3. Environment Sprites

Generate sets of environmental elements using `generateEnvironmentSprites()`. Options include:

- Number of elements
- Theme (e.g., fantasy, sci-fi)
- Art style

### 4. Item Sprites

Create collections of item sprites for game inventories with `generateItemSprites()`. Customize:

- Item count
- Item type (e.g., equipment, consumables)
- Art style

## Advanced Usage

### Fetching Available Options

SpriteAI provides functions to fetch available animation states and sprite styles:

```javascript
import { fetchAvailableAnimationStates, fetchAvailableSpriteStyles } from 'spriteai';

async function getOptions() {
  const states = await fetchAvailableAnimationStates();
  const styles = await fetchAvailableSpriteStyles();

  console.log('Available animation states:', states);
  console.log('Available sprite styles:', styles);
}

getOptions();
```

### Removing Backgrounds

For landscape sprites, you can automatically remove the background:

```javascript
import { generateLandscapeSprite } from 'spriteai';

async function createLandscape() {
  const result = await generateLandscapeSprite('a lush forest', {
    removeBackground: true,
    backgroundColor: '#FFFFFF',
    colorThreshold: 0.1
  });

  console.log('Landscape generated:', result.landscape);
}

createLandscape();
```

## Best Practices

- Be specific in your descriptions to get the best results.
- Experiment with different styles and settings to find what works best for your game.
- Always handle promises and potential errors when using async functions.
- Save generated assets to files for reuse and to avoid unnecessary API calls.

## Next Steps

Now that you're familiar with the basics of SpriteAI, explore the individual function documentation for more detailed information on each feature. Happy asset generation!