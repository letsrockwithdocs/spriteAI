# Troubleshooting Guide for SpriteAI

This guide addresses common issues that users might encounter when using SpriteAI, including error messages, unexpected results, and performance problems. Below, you'll find solutions and workarounds for each issue.

## Table of Contents
1. [OpenAI API Errors](#openai-api-errors)
2. [Image Generation Issues](#image-generation-issues)
3. [Background Removal Problems](#background-removal-problems)
4. [Performance Optimization](#performance-optimization)
5. [File Saving Errors](#file-saving-errors)

## OpenAI API Errors

### Error: "Authentication failed"
**Cause**: Invalid or missing API key.

**Solution**:
1. Ensure you have set up your OpenAI API key correctly.
2. Check if the API key is properly configured in your environment variables or configuration file.
3. Verify that the API key has not expired or been revoked.

### Error: "Rate limit exceeded"
**Cause**: Too many requests in a short period.

**Solution**:
1. Implement rate limiting in your application to avoid exceeding OpenAI's rate limits.
2. Use exponential backoff when retrying failed requests.
3. Consider upgrading your OpenAI plan for higher rate limits if needed.

## Image Generation Issues

### Problem: Inconsistent character sizes across frames
**Cause**: Variations in DALL-E 3 output.

**Solution**:
1. Adjust the prompt to emphasize consistent character size:

```javascript
const prompt = `Create a ${style} character spritesheet of ${description} with these animation states: ${statesDescription}.
  Each row should be a different animation state with ${framesPerState} frames.
  Character should face ${direction}.
  Style requirements:
  - Clean pixel art style
  - Strictly consistent character size across all frames
  - ...`;
```

2. If the issue persists, consider post-processing the generated images to ensure consistent sizing.

### Problem: Blurry or low-quality sprites
**Cause**: Incorrect size parameter or image processing issues.

**Solution**:
1. Verify that the `size` parameter in the `generateCharacterSpritesheet` function is set correctly:

```javascript
const size = '1024x1024';
```

2. Ensure that the image processing libraries (sharp, Jimp) are up-to-date.
3. If using image compression, adjust the quality settings to maintain sprite clarity.

## Background Removal Problems

### Error: "Cannot read property 'bitmap' of undefined"
**Cause**: Failed to read the input image file.

**Solution**:
1. Check if the input file exists and has the correct permissions.
2. Verify that the file path is correct and uses the appropriate path separator for your operating system.
3. Ensure that the image format is supported by Jimp (JPEG, PNG, BMP, TIFF, or GIF).

### Problem: Background not fully removed
**Cause**: Incorrect color threshold or complex backgrounds.

**Solution**:
1. Adjust the `colorThreshold` parameter in the `removeBackgroundColor` function:

```javascript
await removeBackgroundColor(
  tempInputPath, 
  tempOutputPath, 
  options.backgroundColor || '#FFFFFF', 
  options.colorThreshold || 0.2  // Increase this value for more aggressive removal
);
```

2. For complex backgrounds, consider using more advanced image segmentation techniques or third-party services specializing in background removal.

## Performance Optimization

### Problem: Slow sprite generation
**Cause**: Large number of API calls or inefficient image processing.

**Solution**:
1. Implement caching for frequently generated sprites to reduce API calls.
2. Use batch processing for multiple sprites when possible.
3. Optimize image processing operations:

```javascript
// Example: Optimize sharp operations
await sharp(imgBuffer)
  .resize(1024, 1024, { fit: 'inside' })
  .png({ compressionLevel: 9, adaptiveFiltering: true, force: true })
  .toFile(filename);
```

4. Consider using worker threads for parallel processing of multiple sprites.

## File Saving Errors

### Error: "ENOENT: no such file or directory"
**Cause**: Attempting to save files to a non-existent directory.

**Solution**:
1. Ensure that the target directory exists before saving files:

```javascript
import fs from 'fs';
import path from 'path';

// ...

const assetsDir = path.join(process.cwd(), 'assets');
if (!fs.existsSync(assetsDir)) {
  fs.mkdirSync(assetsDir, { recursive: true });
}

const filename = path.join(assetsDir, `${description.replace(/\s+/g, '_')}_spritesheet.png`);
await sharp(spritesheet).toFile(filename);
```

2. Use absolute paths when specifying file locations to avoid relative path issues.

### Error: "EACCES: permission denied"
**Cause**: Insufficient permissions to write files in the target directory.

**Solution**:
1. Check and adjust the permissions of the target directory.
2. Ensure that your application has the necessary write permissions.
3. If running in a containerized environment, verify that the container has appropriate file system access.

By addressing these common issues and following the provided solutions, you should be able to resolve most problems encountered when using SpriteAI. If you continue to experience difficulties, please consult the API documentation or reach out to our support team for further assistance.