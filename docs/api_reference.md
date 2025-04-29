# SpriteAI API Reference

This document provides a detailed API reference for the SpriteAI library, including both main library functions and SDK functions.

## Main Library Functions

### generateCharacterSpritesheet

Generates a character spritesheet based on the provided description and options.

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

#### Parameters:
- `description` (string): A description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (array of strings, default: ['idle', 'walk', 'run', 'attack']): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the spritesheet.
  - `padding` (number, default: 1): Padding between sprites.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean): Whether to save the generated image to the file system.

#### Returns:
An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded spritesheet image.
- `metadata` (object): Metadata about the generated spritesheet.

#### Example:
```javascript
const result = await generateCharacterSpritesheet('a knight in armor', {
  states: ['idle', 'walk', 'attack'],
  framesPerState: 4,
  size: '512x512'
});
console.log(result.metadata);
```

### generateLandscapeSprite

Generates a landscape sprite based on the provided description and options.

```javascript
async function generateLandscapeSprite(description, options = {})
```

#### Parameters:
- `description` (string): A description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the sprite.
  - `timeOfDay` (string, default: 'day'): Time of day setting (day, night, sunset, dawn).
  - `weather` (string, default: 'clear'): Weather conditions (clear, rainy, foggy, snowy).
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (side-scrolling, top-down, isometric).
  - `save` (boolean, default: false): Whether to save the generated image to the file system.
  - `removeBackground` (boolean): Whether to remove the background of the generated image.
  - `backgroundColor` (string): Background color to remove (if removeBackground is true).
  - `colorThreshold` (number): Threshold for background color removal.

#### Returns:
An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded landscape sprite image.
- `metadata` (object): Metadata about the generated landscape sprite.

#### Example:
```javascript
const result = await generateLandscapeSprite('a lush forest with a river', {
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  removeBackground: true,
  backgroundColor: '#FFFFFF'
});
console.log(result.metadata);
```

## SDK Functions

### fetchAvailableAnimationStates

Retrieves a list of available animation states for character spritesheets.

```javascript
async function fetchAvailableAnimationStates()
```

#### Returns:
An array of strings representing available animation states.

#### Example:
```javascript
const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### fetchAvailableSpriteStyles

Retrieves a list of available sprite styles.

```javascript
async function fetchAvailableSpriteStyles()
```

#### Returns:
An array of strings representing available sprite styles.

#### Example:
```javascript
const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

### generateEnvironmentSprites

Generates a tileset of environment sprites based on the provided description and options.

```javascript
async function generateEnvironmentSprites(description, options = {})
```

#### Parameters:
- `description` (string): A description of the environment to generate.
- `options` (object, optional): Configuration options for the environment sprites generation.
  - `elements` (number, default: 4): Number of different elements to generate.
  - `size` (string, default: '1024x1024'): Output size of the tileset.
  - `style` (string, default: 'pixel-art'): Art style of the sprites.
  - `padding` (number, default: 1): Padding between sprite elements.
  - `theme` (string, default: 'fantasy'): Theme of the environment.
  - `save` (boolean): Whether to save the generated image to the file system.

#### Returns:
An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded tileset image.
- `metadata` (object): Metadata about the generated environment sprites.

#### Example:
```javascript
const result = await generateEnvironmentSprites('desert oasis', {
  elements: 6,
  style: 'pixel-art',
  theme: 'desert'
});
console.log(result.metadata);
```

### generateItemSprites

Generates a collection of item sprites based on the provided description and options.

```javascript
async function generateItemSprites(description, options = {})
```

#### Parameters:
- `description` (string): A description of the items to generate.
- `options` (object, optional): Configuration options for the item sprites generation.
  - `itemCount` (number, default: 4): Number of different items to generate.
  - `size` (string, default: '1024x1024'): Output size of the item sheet.
  - `style` (string, default: 'pixel-art'): Art style of the sprites.
  - `padding` (number, default: 1): Padding between item sprites.
  - `itemType` (string, default: 'equipment'): Type of items to generate.
  - `background` (string, default: 'white'): Background color of the item sheet.
  - `save` (boolean): Whether to save the generated image to the file system.

#### Returns:
An object containing:
- `original` (string): URL of the original generated image.
- `itemSheet` (string): Base64-encoded item sheet image.
- `metadata` (object): Metadata about the generated item sprites.

#### Example:
```javascript
const result = await generateItemSprites('magical potions', {
  itemCount: 6,
  style: 'pixel-art',
  itemType: 'consumable',
  background: 'transparent'
});
console.log(result.metadata);
```

## Utility Functions

### removeBackgroundColor

Removes a specified background color from an image.

```javascript
async function removeBackgroundColor(inputPath, outputPath, targetColor, colorThreshold = 0, options = {})
```

#### Parameters:
- `inputPath` (string): Path to the input image file.
- `outputPath` (string): Path where the output image will be saved.
- `targetColor` (string): Color to be removed (e.g., '#FFFFFF').
- `colorThreshold` (number, default: 0): Tolerance for color matching.
- `options` (object, optional): Additional options for background removal.

#### Returns:
A Promise that resolves when the background removal is complete.

#### Example:
```javascript
await removeBackgroundColor('input.png', 'output.png', '#FFFFFF', 0.1);
```

This API reference provides a comprehensive overview of the main functions available in the SpriteAI library. For more detailed information on specific use cases or advanced configurations, please refer to the individual function documentation or examples in the codebase.