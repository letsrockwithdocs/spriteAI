# Getting Started with SpriteAI

Welcome to SpriteAI! This guide will help you get started with our powerful tool for generating game assets using AI. Whether you're a game developer, designer, or hobbyist, SpriteAI can help you create stunning character spritesheets, environment sprites, and item sprites with ease.

## Table of Contents

1. [Installation](#installation)
2. [Basic Usage](#basic-usage)
3. [Main Features](#main-features)
   - [Character Spritesheets](#character-spritesheets)
   - [Environment Sprites](#environment-sprites)
   - [Item Sprites](#item-sprites)
4. [Advanced Options](#advanced-options)
5. [Next Steps](#next-steps)

## Installation

To get started with SpriteAI, you'll need to have Node.js installed on your system. Then, follow these steps:

1. Create a new directory for your project:
   ```
   mkdir my-spriteai-project
   cd my-spriteai-project
   ```

2. Initialize a new Node.js project:
   ```
   npm init -y
   ```

3. Install SpriteAI and its dependencies:
   ```
   npm install spriteai openai axios sharp jimp
   ```

4. Create a new JavaScript file (e.g., `index.js`) in your project directory to start using SpriteAI.

## Basic Usage

Here's a simple example to generate a character spritesheet:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

async function generateSprite() {
  try {
    const result = await generateCharacterSpritesheet('a cute robot character');
    console.log('Spritesheet generated:', result.spritesheet);
    console.log('Metadata:', result.metadata);
  } catch (error) {
    console.error('Error generating spritesheet:', error);
  }
}

generateSprite();
```

This script will generate a spritesheet for a cute robot character with default animation states and options.

## Main Features

SpriteAI offers three main features for generating game assets:

### Character Spritesheets

Generate animated character spritesheets with multiple states like idle, walk, run, and attack.

Example:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

const options = {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  direction: 'right'
};

const result = await generateCharacterSpritesheet('a brave knight', options);
```

### Environment Sprites

Create tileset-style environment sprites for your game backgrounds and levels.

Example:

```javascript
import { generateEnvironmentSprites } from 'spriteai';

const options = {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  theme: 'fantasy'
};

const result = await generateEnvironmentSprites('forest elements', options);
```

### Item Sprites

Generate collections of item sprites for game inventories or pickups.

Example:

```javascript
import { generateItemSprites } from 'spriteai';

const options = {
  itemCount: 4,
  size: '1024x1024',
  style: 'pixel-art',
  itemType: 'equipment'
};

const result = await generateItemSprites('magical weapons', options);
```

## Advanced Options

SpriteAI provides various options to customize your generated sprites:

- `size`: Set the output image size (e.g., '1024x1024')
- `style`: Choose the art style (e.g., 'pixel-art', 'vector', '3d')
- `padding`: Add padding between sprites
- `save`: Automatically save the generated image to the assets folder

For character spritesheets:
- `states`: Define custom animation states
- `framesPerState`: Set the number of frames per animation state
- `direction`: Specify the character's facing direction

For environment sprites:
- `elements`: Set the number of environment elements to generate
- `theme`: Choose a theme for the environment (e.g., 'fantasy', 'sci-fi')

For item sprites:
- `itemCount`: Specify the number of items to generate
- `itemType`: Set the type of items (e.g., 'equipment', 'consumables')

## Next Steps

Now that you're familiar with the basics of SpriteAI, you can start experimenting with different descriptions and options to create unique assets for your game. Here are some suggestions for further exploration:

1. Try generating characters in different styles and with various animation states.
2. Experiment with environment sprites to create diverse game worlds.
3. Create sets of themed item sprites for your game's inventory system.
4. Explore the advanced options to fine-tune your generated assets.

Remember to refer to the API documentation for detailed information on all available functions and options. Happy sprite generating!