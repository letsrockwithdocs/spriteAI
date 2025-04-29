# Advanced Usage Guide for SpriteAI

## Table of Contents
1. [Customizing Sprite Generation](#customizing-sprite-generation)
2. [Working with Different Art Styles](#working-with-different-art-styles)
3. [Optimizing Performance](#optimizing-performance)
4. [Integrating SpriteAI into Game Development Workflows](#integrating-spriteai-into-game-development-workflows)

## Customizing Sprite Generation

SpriteAI offers various options to customize your sprite generation process. Here are some advanced techniques to get the most out of the library:

### Modifying Animation States

By default, the `generateCharacterSpritesheet` function uses predefined animation states. You can customize these states to fit your game's needs:

```javascript
const customStates = ['idle', 'walk', 'jump', 'attack', 'die'];
const result = await generateCharacterSpritesheet('warrior', {
  states: customStates,
  framesPerState: 8
});
```

### Adjusting Sprite Size and Padding

For more control over the generated spritesheet, you can adjust the size and padding:

```javascript
const result = await generateCharacterSpritesheet('mage', {
  size: '2048x2048',
  padding: 2
});
```

### Customizing Character Direction

You can specify the direction the character should face:

```javascript
const result = await generateCharacterSpritesheet('archer', {
  direction: 'left'
});
```

## Working with Different Art Styles

SpriteAI supports various art styles for both character and environment sprites. Here's how to leverage different styles:

### Character Sprites

Use the `style` option to specify different art styles:

```javascript
const pixelArtSprite = await generateCharacterSpritesheet('knight', {
  style: 'pixel-art'
});

const vectorSprite = await generateCharacterSpritesheet('knight', {
  style: 'vector'
});
```

### Environment Sprites

For environment sprites, you can combine style and theme options:

```javascript
const fantasyEnvironment = await generateEnvironmentSprites('forest', {
  style: 'pixel-art',
  theme: 'fantasy'
});

const scifiEnvironment = await generateEnvironmentSprites('space station', {
  style: 'vector',
  theme: 'sci-fi'
});
```

## Optimizing Performance

To improve performance when working with SpriteAI, consider the following techniques:

### Caching Generated Sprites

Implement a caching mechanism to store and reuse generated sprites:

```javascript
const spriteCache = new Map();

async function getCachedSprite(description, options) {
  const cacheKey = JSON.stringify({ description, options });
  
  if (spriteCache.has(cacheKey)) {
    return spriteCache.get(cacheKey);
  }

  const sprite = await generateCharacterSpritesheet(description, options);
  spriteCache.set(cacheKey, sprite);
  return sprite;
}
```

### Batch Processing

When generating multiple sprites, use Promise.all for parallel processing:

```javascript
const spriteDescriptions = ['warrior', 'mage', 'archer', 'thief'];
const spritePromises = spriteDescriptions.map(desc => generateCharacterSpritesheet(desc));

const sprites = await Promise.all(spritePromises);
```

## Integrating SpriteAI into Game Development Workflows

Here are some tips for effectively integrating SpriteAI into your game development process:

### Automated Asset Generation

Create a script to automatically generate and save sprites during your build process:

```javascript
import { generateCharacterSpritesheet, generateEnvironmentSprites } from 'spriteai';
import fs from 'fs/promises';

async function generateGameAssets() {
  const characters = ['player', 'enemy1', 'enemy2', 'npc'];
  const environments = ['forest', 'dungeon', 'town'];

  for (const char of characters) {
    const sprite = await generateCharacterSpritesheet(char, { save: true });
    await fs.writeFile(`./assets/${char}_metadata.json`, JSON.stringify(sprite.metadata));
  }

  for (const env of environments) {
    const sprite = await generateEnvironmentSprites(env, { save: true });
    await fs.writeFile(`./assets/${env}_metadata.json`, JSON.stringify(sprite.metadata));
  }
}

generateGameAssets();
```

### Dynamic Sprite Generation

For games with procedurally generated content, you can use SpriteAI to create sprites on-the-fly:

```javascript
async function createRandomEnemy(level) {
  const enemyTypes = ['goblin', 'orc', 'troll', 'dragon'];
  const randomType = enemyTypes[Math.floor(Math.random() * enemyTypes.length)];
  
  const sprite = await generateCharacterSpritesheet(`level ${level} ${randomType}`);
  
  return {
    type: randomType,
    level: level,
    sprite: sprite.spritesheet,
    animations: sprite.metadata.frameData
  };
}
```

By leveraging these advanced techniques, you can fully utilize the power of SpriteAI in your game development projects, creating dynamic and visually appealing games with ease.