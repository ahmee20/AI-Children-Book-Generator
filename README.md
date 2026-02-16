# AI Children's Book Generator Workflow (n8n)

This project is an end-to-end automated AI-powered children's storybook generator built using n8n.

It takes a child's reference image and story inputs, analyzes facial features using computer vision APIs, and generates a fully illustrated personalized children's book with consistent character appearance across all scenes.

## Features

- Upload a child's reference image via webhook
- Extract facial attributes and landmarks using:
  - Face detection
  - Emotion analysis
  - Eye status
  - Skin condition
  - Head pose
- Detect visual traits and objects in the image
- Convert raw API responses into natural human-readable descriptions
- Maintain facial consistency across all generated images
- Automatically generate:
  - Book Cover Illustration
  - 16 Story Scene Illustrations
  - Story Summary for Cover Page
  - Style-controlled illustration generation (e.g., Ghibli-style)
  - Character appearance consistency across all story scenes

## Workflow Overview

### Image Upload

A webhook endpoint receives:

- Child's reference image URL
- Physical attributes (hair color, eye color, skin tone, etc.)
- Companion information
- Theme/style for the story
- Story universe
- Age & name of child

### Face Analysis (Face++)

The uploaded image is sent to the Face++ API to extract:

- Gender
- Smile detection
- Head pose
- Image quality
- Blur level
- Eye status
- Emotion
- Skin health
- Glasses detection
- Facial landmarks

The extracted attributes are converted into natural language using a Code Node.

### Scene & Object Detection (Google Vision)

Image is analyzed using Google Vision API to detect:

- Facial likelihoods
- Object localization
- Environmental labels
- Visual traits

These results are also converted into readable descriptive data.

### Data Merge

All extracted:

- Facial attributes
- Visual traits
- Objects
- Landmark summaries

are merged to build a consistent reference profile of the child for all future illustrations.

### Landmark Summarization

Important facial landmark coordinates are summarized to maintain:

- Face shape consistency
- Eye placement
- Mouth positioning
- Chin structure
- Nose alignment

This ensures the generated character looks the same in every scene.

### Story Scene Processing

- Story is divided into 16 scenes
- Each scene is converted into a visual description using an LLM
- Output is kept grounded and child-friendly
- Only visible, realistic elements are described for illustration

### Image Generation

For each scene:

- A style-controlled prompt is generated
- Child's appearance is enforced across all images
- Companion is included in scenes
- Background strictly matches the story
- Images are generated using OpenAI Image Models

### Cover Page Generation

- A cinematic children's book cover is generated
- Emotion and mood are extracted from facial analysis
- Character styling is matched with story theme

### Story Summary Generation

All scenes are combined to generate:

- A short 4–5 sentence summary for the book's front page

## Requirements

- n8n Instance (Cloud or Self-hosted)
- Face++ API Key
- Google Vision API Key
- OpenAI API Key
- Publicly accessible image URL input

## How to Use

1. Import the workflow JSON into n8n
2. Add API credentials:
   - Face++
   - Google Vision
   - OpenAI
3. Activate the Webhook node
4. Send a POST request to: `/webhook/image-upload`

### Request Parameters

```json
{
  "image_url": "string",
  "child_name": "string",
  "age": "number",
  "gender": "string",
  "hair_color": "string",
  "hair_type": "string",
  "eye_color": "string",
  "skin_tone": "string",
  "theme": "string",
  "universe": "string",
  "companion": "string"
}
```

## Output

The workflow returns:

- Generated Cover Illustration
- 16 Scene Illustrations
- Book Summary

All visuals maintain character consistency based on the reference image.

## Use Cases

- Personalized Children's Storybooks
- AI-Based Character Illustration
- Story Visualization
- Educational Content Creation
- Custom Comic Generation
