# Troubleshooting Guide for SpriteAI

This guide covers common issues you might encounter when using the SpriteAI library and provides solutions to help you resolve them quickly.

## Table of Contents
1. [Image Generation Issues](#image-generation-issues)
2. [API Errors](#api-errors)
3. [Integration Challenges](#integration-challenges)
4. [Performance Problems](#performance-problems)

## Image Generation Issues

### Problem: Generated sprites are blurry or low-quality

**Possible causes:**
- Incorrect size parameter
- Issues with the DALL-E API

**Solutions:**
1. Check the `size` parameter in your function call:
   ```javascript
   const result = await generateCharacterSpritesheet(description, {
     size: '1024x1024', // Ensure this is set to a supported size
   });
   ```
2. Try regenerating the image with a different prompt or style.
3. Verify that you're using the latest version of the SpriteAI library.

### Problem: Background color isn't removed properly

**Possible causes:**
- Incorrect color threshold
- Complex or gradient backgrounds

**Solutions:**
1. Adjust the `colorThreshold` parameter:
   ```javascript
   await removeBackgroundColor(
     inputPath,
     outputPath,
     '#FFFFFF',
     0.1 // Try adjusting this value
   );
   ```
2. For complex backgrounds, consider using a more advanced image processing library or a dedicated background removal service.

## API Errors

### Problem: OpenAI API key issues

**Possible causes:**
- Missing or invalid API key
- Exceeded API rate limits

**Solutions:**
1. Ensure your OpenAI API key is correctly set in your environment variables:
   ```javascript
   const openAiObject = new OpenAI();
   ```
2. Check your OpenAI account for any usage limits or billing issues.
3. Implement proper error handling to catch and log API-related errors:
   ```javascript
   try {
     const response = await openAiObject.images.generate({
       // ...options
     });
   } catch (error) {
     console.error('OpenAI API Error:', error.message);
     // Handle the error appropriately
   }
   ```

### Problem: "Model not found" error

**Possible causes:**
- Using an unsupported or deprecated model

**Solution:**
Ensure you're using the correct model name. For SpriteAI, we use "dall-e-3":
```javascript
const response = await openAiObject.images.generate({
  model: "dall-e-3",
  // ...other options
});
```

## Integration Challenges

### Problem: Difficulty integrating generated sprites into game engines

**Possible causes:**
- Incompatible image format
- Incorrect sprite dimensions

**Solutions:**
1. Use the `sharp` library to convert the image to a compatible format:
   ```javascript
   import sharp from 'sharp';

   const compatibleBuffer = await sharp(spritesheet)
     .png()
     .toBuffer();
   ```
2. Ensure your game engine's sprite importer settings match the generated sprite dimensions:
   ```javascript
   const metadata = result.metadata;
   console.log(`Sprite dimensions: ${metadata.dimensions.width}x${metadata.dimensions.height}`);
   console.log(`Frames per state: ${metadata.framesPerState}`);
   ```

### Problem: Inconsistent sprite sizes across different generations

**Possible causes:**
- Variations in DALL-E output
- Inconsistent prompts

**Solutions:**
1. Use more specific prompts to ensure consistent character sizes:
   ```javascript
   const prompt = `Create a ${style} character spritesheet of ${description} with these animation states: ${statesDescription}.
     Each row should be a different animation state with ${framesPerState} frames.
     Character should face ${direction}.
     Style requirements:
     - Clean pixel art style
     - Consistent character size across all frames (exactly 64x64 pixels per frame)
     ...`;
   ```
2. Implement post-processing to normalize sprite sizes:
   ```javascript
   import sharp from 'sharp';

   const normalizedSpritesheet = await sharp(spritesheet)
     .resize(64 * framesPerState, 64 * states.length)
     .toBuffer();
   ```

## Performance Problems

### Problem: Slow sprite generation

**Possible causes:**
- Network latency
- Large image sizes
- Complex prompts

**Solutions:**
1. Implement caching for frequently used sprites:
   ```javascript
   import NodeCache from 'node-cache';

   const spriteCache = new NodeCache({ stdTTL: 3600 }); // Cache for 1 hour

   export const generateCharacterSpritesheet = async function(description, options = {}) {
     const cacheKey = `${description}-${JSON.stringify(options)}`;
     const cachedResult = spriteCache.get(cacheKey);
     
     if (cachedResult) {
       return cachedResult;
     }

     // Generate sprite as normal
     const result = // ... generation code ...

     spriteCache.set(cacheKey, result);
     return result;
   };
   ```
2. Use smaller image sizes when high resolution isn't necessary:
   ```javascript
   const result = await generateCharacterSpritesheet(description, {
     size: '512x512', // Use smaller size for faster generation
   });
   ```
3. Optimize prompts to be more concise while still achieving desired results.

By following this troubleshooting guide, you should be able to resolve most common issues encountered when using the SpriteAI library. If you continue to experience problems, please check the GitHub repository for known issues or open a new issue with a detailed description of your problem.