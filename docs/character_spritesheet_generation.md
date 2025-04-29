# Character Spritesheet Generation

This guide provides a detailed explanation of how to use the `generateCharacterSpritesheet` function to create custom character spritesheets for your game development needs.

## Table of Contents

1. [Overview](#overview)
2. [Function Signature](#function-signature)
3. [Parameters](#parameters)
4. [Options](#options)
5. [Return Value](#return-value)
6. [Usage Examples](#usage-examples)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)

## Overview

The `generateCharacterSpritesheet` function allows you to create pixel art character spritesheets using AI-powered image generation. This function leverages the DALL-E 3 model to generate a complete spritesheet based on your character description and specified animation states.

## Function Signature

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

## Parameters

- `description` (string): A detailed description of the character you want to generate.
- `options` (object): An optional object containing configuration options for the spritesheet generation.

## Options

The `options` object can include the following properties:

- `states` (array of strings): Animation states to generate. Default: `['idle', 'walk', 'run', 'attack']`
- `framesPerState` (number): Number of frames per animation state. Default: `6`
- `size` (string): Output size of the spritesheet. Default: `'1024x1024'`
- `style` (string): Art style of the character. Default: `'pixel-art'`
- `padding` (number): Padding between sprites in the sheet. Default: `1`
- `direction` (string): Base direction the character faces. Default: `'right'`
- `save` (boolean): Whether to save the generated spritesheet to disk. Default: `false`

## Return Value

The function returns a Promise that resolves to an object with the following properties:

- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded data URL of the processed spritesheet.
- `metadata` (object): Metadata about the generated spritesheet, including:
  - `states` (array): List of animation states.
  - `framesPerState` (number): Number of frames per state.
  - `totalFrames` (number): Total number of frames in the spritesheet.
  - `dimensions` (object): Width and height of the spritesheet.
  - `frameData` (object): Detailed information about each animation state's frames.

## Usage Examples

### Basic Usage

```javascript
import { generateCharacterSpritesheet } from './spriteAI';

async function createBasicCharacter() {
  const result = await generateCharacterSpritesheet('A cute pixelated cat warrior');
  console.log(result.spritesheet); // Base64 encoded spritesheet
  console.log(result.metadata); // Metadata about the spritesheet
}

createBasicCharacter();
```

### Custom Animation States

```javascript
async function createCustomCharacter() {
  const options = {
    states: ['idle', 'walk', 'jump', 'attack', 'die'],
    framesPerState: 8,
    size: '2048x2048',
    style: 'pixel-art',
    direction: 'left'
  };

  const result = await generateCharacterSpritesheet('A fierce orc shaman', options);
  console.log(result.metadata.frameData);
}

createCustomCharacter();
```

### Saving the Spritesheet

```javascript
async function createAndSaveCharacter() {
  const options = {
    save: true,
    states: ['idle', 'cast', 'teleport'],
    style: 'vector'
  };

  await generateCharacterSpritesheet('A mystical wizard', options);
  console.log('Spritesheet saved to assets folder');
}

createAndSaveCharacter();
```

## Best Practices

1. **Detailed Descriptions**: Provide clear and detailed character descriptions for better results.
2. **Consistent Style**: Keep the art style consistent across different character generations by using the same `style` option.
3. **Appropriate Frame Count**: Choose an appropriate `framesPerState` based on the complexity of your animations.
4. **Optimize Size**: Use the `size` option to generate spritesheets that match your game's resolution requirements.
5. **Test Different Options**: Experiment with different combinations of options to achieve the desired results.

## Troubleshooting

- If the generated spritesheet doesn't match your expectations, try adjusting the character description or options.
- Ensure you have the necessary permissions and API keys set up for using the DALL-E 3 model.
- If saving fails, check that the specified save directory exists and has write permissions.
- For performance issues, consider reducing the `size` or `framesPerState` options.

Remember that AI-generated content may require additional editing or refinement to fully match your game's aesthetic and functional requirements.