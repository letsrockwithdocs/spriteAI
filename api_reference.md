# SpriteAI API Reference

This document provides a comprehensive reference for the SpriteAI library, detailing all public functions, their parameters, return values, and usage examples. The API is organized into the following main categories:

- [Character Sprites](#character-sprites)
- [Landscape Sprites](#landscape-sprites)
- [Environment Sprites](#environment-sprites)
- [Item Sprites](#item-sprites)
- [Utility Functions](#utility-functions)

## Character Sprites

### generateCharacterSpritesheet

Generates a character spritesheet with multiple animation states.

#### Parameters

- `description` (string): A description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet.
  - `states` (array of strings, default: `['idle', 'walk', 'run', 'attack']`): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the character.
  - `padding` (number, default: 1): Padding between sprites.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean): Whether to save the generated image to disk.

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded data URL of the processed spritesheet.
- `metadata` (object): Detailed information about the spritesheet, including states, frame data, and dimensions.

#### Example

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const result = await generateCharacterSpritesheet('a medieval knight', {
  states: ['idle', 'walk', 'attack', 'defend'],
  framesPerState: 8,
  style: 'pixel-art',
  save: true
});

console.log(result.metadata);
// Use result.spritesheet for rendering in your game
```

## Landscape Sprites

### generateLandscapeSprite

Generates a landscape sprite suitable for use as a game background.

#### Parameters

- `description` (string): A description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape sprite.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the landscape.
  - `timeOfDay` (string, default: 'day'): Time of day setting (day, night, sunset, dawn).
  - `weather` (string, default: 'clear'): Weather conditions (clear, rainy, foggy, snowy).
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (side-scrolling, top-down, isometric).
  - `save` (boolean, default: false): Whether to save the generated image to disk.
  - `removeBackground` (boolean): Whether to remove the background color.
  - `backgroundColor` (string): Target background color to remove (if removeBackground is true).
  - `colorThreshold` (number): Threshold for color removal (if removeBackground is true).

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded data URL of the processed landscape sprite.
- `metadata` (object): Detailed information about the landscape, including description, style, time of day, weather, perspective, and dimensions.

#### Example

```javascript
import { generateLandscapeSprite } from 'spriteAI';

const result = await generateLandscapeSprite('a lush forest with a winding river', {
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true,
  backgroundColor: '#FFFFFF'
});

console.log(result.metadata);
// Use result.landscape for rendering in your game
```

## Environment Sprites

### generateEnvironmentSprites

Generates a tileset of environment sprites for game levels.

#### Parameters

- `description` (string): A description of the environment to generate.
- `options` (object, optional): Configuration options for the environment sprites.
  - `elements` (number, default: 4): Number of different elements to generate.
  - `size` (string, default: '1024x1024'): Output size of the tileset.
  - `style` (string, default: 'pixel-art'): Art style of the environment sprites.
  - `padding` (number, default: 1): Padding between sprites.
  - `theme` (string, default: 'fantasy'): Theme of the environment.
  - `save` (boolean): Whether to save the generated image to disk.

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded data URL of the processed environment tileset.
- `metadata` (object): Detailed information about the tileset, including number of elements, theme, dimensions, and tile data.

#### Example

```javascript
import { generateEnvironmentSprites } from 'spriteAI';

const result = await generateEnvironmentSprites('desert oasis', {
  elements: 6,
  style: 'pixel-art',
  theme: 'desert',
  save: true
});

console.log(result.metadata);
// Use result.tileset for rendering in your game level editor
```

## Item Sprites

### generateItemSprites

Generates a collection of item sprites for game inventories or pickups.

#### Parameters

- `description` (string): A description of the items to generate.
- `options` (object, optional): Configuration options for the item sprites.
  - `itemCount` (number, default: 4): Number of different items to generate.
  - `size` (string, default: '1024x1024'): Output size of the item sheet.
  - `style` (string, default: 'pixel-art'): Art style of the item sprites.
  - `padding` (number, default: 1): Padding between sprites.
  - `itemType` (string, default: 'equipment'): Type of items to generate.
  - `background` (string, default: 'white'): Background color of the item sheet.
  - `save` (boolean): Whether to save the generated image to disk.

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `itemSheet` (string): Base64-encoded data URL of the processed item sheet.
- `metadata` (object): Detailed information about the item sheet, including item count, item type, dimensions, and item data.

#### Example

```javascript
import { generateItemSprites } from 'spriteAI';

const result = await generateItemSprites('magical artifacts', {
  itemCount: 8,
  style: 'pixel-art',
  itemType: 'magical',
  save: true
});

console.log(result.metadata);
// Use result.itemSheet for rendering in your game inventory system
```

## Utility Functions

### fetchAvailableAnimationStates

Retrieves a list of available animation states for character sprites.

#### Returns

An array of strings representing available animation states.

#### Example

```javascript
import { fetchAvailableAnimationStates } from 'spriteAI';

const states = await fetchAvailableAnimationStates();
console.log(states);
// Output: ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### fetchAvailableSpriteStyles

Retrieves a list of available sprite styles.

#### Returns

An array of strings representing available sprite styles.

#### Example

```javascript
import { fetchAvailableSpriteStyles } from 'spriteAI';

const styles = await fetchAvailableSpriteStyles();
console.log(styles);
// Output: ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

This concludes the API reference for SpriteAI. For more detailed information on implementation and advanced usage, please refer to the main documentation and tutorials.