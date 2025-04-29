# Configuration Options

This guide provides a comprehensive overview of all configuration options available in the SpriteAI library. Understanding these options will help you customize the sprite generation process to suit your specific needs.

## Character Spritesheet Generation

The `generateCharacterSpritesheet` function accepts the following configuration options:

### states
- **Type**: Array of strings
- **Default**: `['idle', 'walk', 'run', 'attack']`
- **Description**: Defines the animation states to generate for the character.
- **Example**:
  ```javascript
  states: ['idle', 'walk', 'run', 'attack', 'jump']
  ```

### framesPerState
- **Type**: Number
- **Default**: `6`
- **Description**: Specifies the number of frames to generate for each animation state.
- **Example**:
  ```javascript
  framesPerState: 8
  ```

### size
- **Type**: String
- **Default**: `'1024x1024'`
- **Description**: Sets the output size of the generated spritesheet.
- **Example**:
  ```javascript
  size: '2048x2048'
  ```

### style
- **Type**: String
- **Default**: `'pixel-art'`
- **Description**: Determines the art style of the generated sprites.
- **Example**:
  ```javascript
  style: 'vector'
  ```

### padding
- **Type**: Number
- **Default**: `1`
- **Description**: Defines the padding between individual sprites in the spritesheet.
- **Example**:
  ```javascript
  padding: 2
  ```

### direction
- **Type**: String
- **Default**: `'right'`
- **Description**: Sets the base direction the character faces in the spritesheet.
- **Example**:
  ```javascript
  direction: 'left'
  ```

### save
- **Type**: Boolean
- **Default**: `false`
- **Description**: When set to `true`, saves the generated spritesheet to the local file system.
- **Example**:
  ```javascript
  save: true
  ```

## Landscape Sprite Generation

The `generateLandscapeSprite` function supports these configuration options:

### size
- **Type**: String
- **Default**: `'1024x1024'`
- **Description**: Sets the output size of the generated landscape sprite.
- **Example**:
  ```javascript
  size: '2048x1024'
  ```

### style
- **Type**: String
- **Default**: `'pixel-art'`
- **Description**: Determines the art style of the generated landscape.
- **Example**:
  ```javascript
  style: 'hand-drawn'
  ```

### timeOfDay
- **Type**: String
- **Default**: `'day'`
- **Description**: Specifies the time of day for the landscape scene.
- **Options**: `'day'`, `'night'`, `'sunset'`, `'dawn'`
- **Example**:
  ```javascript
  timeOfDay: 'sunset'
  ```

### weather
- **Type**: String
- **Default**: `'clear'`
- **Description**: Sets the weather conditions for the landscape scene.
- **Options**: `'clear'`, `'rainy'`, `'foggy'`, `'snowy'`
- **Example**:
  ```javascript
  weather: 'rainy'
  ```

### perspective
- **Type**: String
- **Default**: `'side-scrolling'`
- **Description**: Defines the perspective of the landscape scene.
- **Options**: `'side-scrolling'`, `'top-down'`, `'isometric'`
- **Example**:
  ```javascript
  perspective: 'isometric'
  ```

### save
- **Type**: Boolean
- **Default**: `false`
- **Description**: When set to `true`, saves the generated landscape sprite to the local file system.
- **Example**:
  ```javascript
  save: true
  ```

### removeBackground
- **Type**: Boolean
- **Default**: `false`
- **Description**: When set to `true`, attempts to remove the background from the generated sprite.
- **Example**:
  ```javascript
  removeBackground: true
  ```

### backgroundColor
- **Type**: String
- **Default**: `'#FFFFFF'`
- **Description**: Specifies the background color to remove when `removeBackground` is `true`.
- **Example**:
  ```javascript
  backgroundColor: '#000000'
  ```

### colorThreshold
- **Type**: Number
- **Default**: `0.1`
- **Description**: Sets the threshold for color difference when removing the background.
- **Example**:
  ```javascript
  colorThreshold: 0.2
  ```

## Common Configuration Examples

### Generate a pixel-art character spritesheet with custom states
```javascript
const options = {
  states: ['idle', 'walk', 'run', 'jump', 'attack'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  save: true
};

const result = await generateCharacterSpritesheet('warrior', options);
```

### Create a landscape sprite with specific weather and time of day
```javascript
const options = {
  size: '1024x512',
  style: 'hand-drawn',
  timeOfDay: 'sunset',
  weather: 'foggy',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true
};

const result = await generateLandscapeSprite('mystical forest', options);
```

By utilizing these configuration options, you can fine-tune the sprite generation process to create assets that perfectly fit your game's visual style and requirements.