# Troubleshooting Guide for SpriteAI

This guide addresses common issues users might encounter when using SpriteAI and provides step-by-step solutions for resolving them. If you're experiencing problems with image generation, API usage, or integration with other tools, you'll find helpful information here.

## Table of Contents

1. [Image Generation Issues](#image-generation-issues)
2. [API Usage Problems](#api-usage-problems)
3. [Integration Challenges](#integration-challenges)
4. [Performance Concerns](#performance-concerns)

## Image Generation Issues

### 1. Blank or Incomplete Spritesheets

**Problem:** The generated spritesheet is blank or missing some frames.

**Solution:**
1. Check your `description` parameter to ensure it's clear and specific.
2. Verify that the `states` array in your options contains valid animation states.
3. Increase the `size` parameter to allow for more detailed sprites.

Example:

```javascript
const result = await generateCharacterSpritesheet("a red dragon", {
  states: ['idle', 'walk', 'attack'],
  size: '1024x1024',
  style: 'pixel-art'
});
```

### 2. Inconsistent Character Size Across Frames

**Problem:** The character size varies between different animation frames.

**Solution:**
1. Emphasize consistency in your prompt by adding "Ensure consistent character size across all frames" to the description.
2. Use the `padding` option to provide more space between frames.

Example:

```javascript
const result = await generateCharacterSpritesheet("a consistent-sized knight", {
  padding: 2,
  framesPerState: 4
});
```

## API Usage Problems

### 1. Authentication Errors

**Problem:** Receiving "Authentication failed" or "Invalid API key" errors.

**Solution:**
1. Verify that you've set up your OpenAI API key correctly.
2. Check if the API key is properly loaded in your environment variables.
3. Ensure you're using the latest version of the `openai` package.

Example of setting up the API key:

```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY
});
```

### 2. Rate Limiting Issues

**Problem:** Encountering "Rate limit exceeded" errors.

**Solution:**
1. Implement exponential backoff and retry logic in your requests.
2. Consider using a queueing system for high-volume operations.
3. Monitor your API usage and adjust your requests accordingly.

Example of implementing simple retry logic:

```javascript
const MAX_RETRIES = 3;
const RETRY_DELAY = 1000; // 1 second

async function generateWithRetry(description, options, retries = 0) {
  try {
    return await generateCharacterSpritesheet(description, options);
  } catch (error) {
    if (error.message.includes('Rate limit exceeded') && retries < MAX_RETRIES) {
      await new Promise(resolve => setTimeout(resolve, RETRY_DELAY * Math.pow(2, retries)));
      return generateWithRetry(description, options, retries + 1);
    }
    throw error;
  }
}
```

## Integration Challenges

### 1. Incompatible Image Formats

**Problem:** Generated images are not compatible with your game engine or framework.

**Solution:**
1. Use the `sharp` library to convert the image to a compatible format.
2. Ensure you're correctly parsing the base64 image data returned by SpriteAI.

Example of converting to PNG:

```javascript
import sharp from 'sharp';

const result = await generateCharacterSpritesheet("a blue mage");
const buffer = Buffer.from(result.spritesheet.split(',')[1], 'base64');

await sharp(buffer)
  .png()
  .toFile('mage_spritesheet.png');
```

### 2. Incorrect Spritesheet Dimensions

**Problem:** The spritesheet dimensions don't match your game's requirements.

**Solution:**
1. Use the `metadata` returned by SpriteAI to calculate the correct frame size.
2. Implement a custom function to slice the spritesheet into individual frames if needed.

Example of calculating frame dimensions:

```javascript
const result = await generateCharacterSpritesheet("a hero character", {
  states: ['idle', 'walk', 'run'],
  framesPerState: 4
});

const { width, height } = result.metadata.dimensions;
const frameWidth = width / result.metadata.framesPerState;
const frameHeight = height / result.metadata.states.length;

console.log(`Each frame is ${frameWidth}x${frameHeight} pixels`);
```

## Performance Concerns

### 1. Slow Generation Times

**Problem:** Sprite generation is taking too long for real-time use.

**Solution:**
1. Implement caching for frequently used sprites.
2. Generate sprites in advance and store them, rather than generating on-demand.
3. Optimize your prompts to be more specific, potentially reducing generation time.

Example of a simple caching mechanism:

```javascript
const spriteCache = new Map();

async function getCachedSprite(description, options) {
  const cacheKey = JSON.stringify({ description, options });
  if (spriteCache.has(cacheKey)) {
    return spriteCache.get(cacheKey);
  }
  
  const result = await generateCharacterSpritesheet(description, options);
  spriteCache.set(cacheKey, result);
  return result;
}
```

### 2. High Memory Usage

**Problem:** The application is using too much memory when generating multiple sprites.

**Solution:**
1. Implement a cleanup function to remove unnecessary data after sprite generation.
2. Use streams for processing large images instead of loading them entirely into memory.
3. Consider using worker threads for parallel processing of multiple sprite generations.

Example of a cleanup function:

```javascript
function cleanupSpriteData(spriteResult) {
  // Remove the original image data to save memory
  delete spriteResult.original;
  
  // Convert base64 spritesheet to a file reference
  const filename = `sprite_${Date.now()}.png`;
  fs.writeFileSync(filename, Buffer.from(spriteResult.spritesheet.split(',')[1], 'base64'));
  spriteResult.spritesheet = filename;
  
  return spriteResult;
}

const result = await generateCharacterSpritesheet("a memory-efficient sprite");
const cleanResult = cleanupSpriteData(result);
```

By following this troubleshooting guide, you should be able to resolve most common issues encountered when using SpriteAI. If you continue to experience problems, please reach out to our support team or consult the API documentation for more detailed information.