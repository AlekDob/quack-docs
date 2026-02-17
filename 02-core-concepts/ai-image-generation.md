AI Image Generation brings visual creativity directly into your workflow. With the `openai image gen` skill, agents can generate custom images, illustrations, and graphics using OpenAI's DALL-E model - perfect for landing pages, marketing materials, documentation, or any project that needs visual assets.

## Overview

When an agent has access to the image generation skill, it can:

- **Generate images from text descriptions** - Natural language prompts
- **Preview inline** - Images appear directly in chat stream
- **Save automatically** - Files stored in project assets folder
- **Open full-size** - One-click viewer for detailed inspection
- **Work autonomously** - Agent handles creative decisions

## Setup

### Requirements

To use AI Image Generation, you need:

1. **OpenAI API Key** - From [platform.openai.com](https://platform.openai.com)
2. **Quack Settings Configuration** - Add key to settings
3. **Image Generation Skill** - Assigned to your agent

### Getting an OpenAI API Key

1. Go to [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
2. Click **Create new secret key**
3. Name it (e.g., "Quack Image Generation")
4. Copy the key (starts with `sk-...`)

### Configuring Quack

1. Open Quack Settings (`Cmd+,` or `Ctrl+,`)
2. Navigate to **AI Assistant** section
3. Find **OpenAI API Key** field
4. Paste your API key
5. Click **Save**

Your API key is:
- **Stored locally** - Never sent to Quack servers
- **Encrypted on macOS** - Uses system keychain
- **Used only for image generation** - Not shared with other services

### Assigning the Skill

The `openai image gen` skill needs to be assigned to your agent:

**Option 1: Via Agent Settings**
1. Open the Agent Context panel
2. Click **Edit Agent**
3. Go to **Skills** section
4. Add `openai image gen` skill
5. Save

**Option 2: Via Rules**
Add to agent's CLAUDE.md or rules:
```
Use the openai image gen skill for visual assets
```

## Generating Images

### Basic Usage

Simply ask the agent to create an image:

```
You: "Create a hero image for our landing page"

Agent: "I'll generate a hero image for your landing page."

[Generating image...]

[Image preview appears inline]

Image saved to: /project/assets/hero-landing-page.png
```

### Providing Details

More specific prompts produce better results:

```
You: "Generate a minimalist illustration of a rocket launching,
      with a gradient background from purple to blue,
      suitable for a SaaS landing page"

Agent: "Generating illustration..."

[Image appears with specified style]
```

### Multiple Images

Request variations or different assets:

```
You: "Create 3 different icon styles for our app:
      1. Modern and minimalist
      2. Playful and colorful
      3. Professional and clean"

Agent: "I'll generate three icon variations..."

[Three images appear in sequence]
```

## Image Preview

### Inline Preview

Generated images appear directly in the chat stream:

```
┌─────────────────────────────────────────────────────┐
│  Agent: "Here's the hero image:"                    │
│                                                      │
│  ┌─────────────────────────────────────┐           │
│  │                                      │           │
│  │    [Generated Image Preview]         │           │
│  │      600x400px thumbnail             │           │
│  │                                      │           │
│  └─────────────────────────────────────┘           │
│                                                      │
│  [Open in tab] hero-landing-page.png                │
└─────────────────────────────────────────────────────┘
```

### Full-Size Viewer

Click **Open in tab** to view the image at full resolution:

- New tab opens with image viewer
- Zoom in/out with mouse wheel
- Pan around the image
- See full metadata (dimensions, prompt, model)

### Image Format

Generated images are:
- **Format**: PNG (lossless, transparent backgrounds supported)
- **Size**: 1024x1024px (default) or custom dimensions
- **Quality**: High-resolution, production-ready

## File Management

### Automatic Saving

Images are automatically saved to your project:

**Default location:**
```
/your-project/assets/images/
```

**File naming:**
- Based on description or content
- Sanitized for filesystem compatibility
- Numbered if duplicates exist

**Example structure:**
```
project/
├── assets/
│   └── images/
│       ├── hero-landing-page.png
│       ├── feature-icon-dashboard.png
│       ├── team-photo-placeholder.png
│       └── background-gradient-blue.png
```

### Custom Paths

Specify where to save:

```
You: "Generate a logo and save it to /public/logo.png"

Agent: "Generating logo and saving to /public/logo.png..."
```

### Organizing Assets

Create organized asset folders:

```
You: "Generate illustration assets for the features section.
      Save them in /assets/features/"

Agent: "I'll create illustrations for each feature..."

Result:
/assets/features/
├── analytics-chart.png
├── collaboration-team.png
└── security-shield.png
```

## Use Cases

### Landing Pages

**Prompt:**
```
"Create a modern, vibrant hero image for a productivity app landing page.
 Include elements like calendars, checkboxes, and notifications.
 Use a gradient from #FF6B35 to #004E89."
```

**Result:** Custom hero image matching your brand colors.

### Documentation

**Prompt:**
```
"Generate a simple diagram showing data flow:
 User → API → Database → Response.
 Use arrows and boxes, keep it minimal."
```

**Result:** Clean visual aid for your docs.

### Placeholder Content

**Prompt:**
```
"Create 5 diverse team member placeholder photos -
 professional headshots with neutral backgrounds"
```

**Result:** Placeholder images for development.

### Marketing Materials

**Prompt:**
```
"Design a social media banner (1200x630) showcasing our new feature.
 Include text space on the left, visual element on the right.
 Professional but friendly style."
```

**Result:** Social media ready graphics.

### App Icons and Assets

**Prompt:**
```
"Generate a set of feature icons for our dashboard:
 - Analytics (chart icon)
 - Settings (gear icon)
 - Users (people icon)
 - Reports (document icon)
 Keep them consistent in style, use single color #004E89"
```

**Result:** Cohesive icon set.

## Advanced Features

### Style Consistency

Maintain visual consistency across images:

```
You: "Use the same style as the previous image but for a different scene"

Agent: *Generates new image matching previous aesthetic*
```

### Iterative Refinement

Refine images through conversation:

```
You: "Make the background lighter"
You: "Add more contrast"
You: "Perfect! Save this version"
```

### Batch Generation

Generate multiple assets efficiently:

```
You: "Generate all the images needed for the landing page:
      - Hero section background
      - 3 feature illustrations
      - Footer decoration
      - About team photo placeholder"

Agent: *Creates all 6 images systematically*
```

### Integration with Website Building

When building sites, agents automatically generate needed visuals:

```
You: "Build a landing page for a fitness app"

Agent:
1. Creates HTML structure
2. Generates hero image with fitness theme
3. Creates feature section icons
4. Generates testimonial avatars
5. Saves all assets to /public/images/
6. Updates HTML to reference generated images
```

## Best Practices

### Writing Effective Prompts

**Be specific about:**
- **Style**: "minimalist", "photorealistic", "illustrated", "abstract"
- **Colors**: Hex codes, color names, or "match brand colors"
- **Mood**: "professional", "playful", "serious", "energetic"
- **Elements**: What should be in the image
- **Purpose**: Where the image will be used

**Good prompt:**
```
"Create a minimalist illustration of a dashboard interface,
 using flat design style with #FF6B35 accent color,
 for a SaaS product hero section"
```

**Vague prompt:**
```
"Make a picture for the website"
```

### When to Generate Images

**Good use cases:**
- Prototyping and mockups
- Placeholder content during development
- Custom illustrations for unique concepts
- Marketing materials
- Social media graphics

**When NOT to use:**
- Photos of real people you know (use real photos)
- Product photography (use actual product photos)
- Logos requiring legal trademark protection
- Content requiring precision accuracy (technical diagrams)

### Cost Awareness

Image generation uses OpenAI credits:
- **Standard**: ~$0.02 per image (1024x1024)
- **HD Quality**: ~$0.08 per image
- Monitor usage in OpenAI dashboard
- Set spending limits if needed

### File Organization

Create a clear structure:

```
project/
├── public/
│   ├── images/          # Public-facing images
│   └── icons/           # UI icons
├── assets/
│   ├── generated/       # AI-generated assets
│   ├── originals/       # Source files
│   └── optimized/       # Compressed versions
```

## Limitations and Considerations

### Content Policy

OpenAI has content policies. Images cannot contain:
- Violence or gore
- Hate symbols
- Adult content
- Copyrighted characters

The agent will reject prompts that violate policies.

### Quality Expectations

AI-generated images are excellent for:
- Conceptual illustrations
- Abstract backgrounds
- Stylized graphics
- Placeholder content

They may not be perfect for:
- Photorealistic specific objects
- Text rendering (text in images may be garbled)
- Precise technical diagrams
- Faces of specific people

### Rate Limits

OpenAI has rate limits:
- ~50 images per minute (standard tier)
- Higher limits with paid plans
- Agent handles rate limiting automatically

## Troubleshooting

### No Images Generated

**Cause**: API key not configured or invalid

**Solution**:
1. Check Settings → AI Assistant → OpenAI API Key
2. Verify key is valid at platform.openai.com
3. Check API key has image generation permissions

### "Content Policy Violation" Error

**Cause**: Prompt violates OpenAI content policy

**Solution**:
- Rephrase the prompt
- Remove potentially problematic words
- Make the request more professional/neutral

### Image Quality Issues

**Cause**: Vague or conflicting prompt

**Solution**:
- Be more specific about style and elements
- Provide reference examples
- Use iterative refinement ("make it lighter", "more contrast")

### Images Not Saving

**Cause**: Permission issues or invalid path

**Solution**:
- Check project folder permissions
- Verify path exists or can be created
- Use relative paths from project root

### Slow Generation

**Cause**: OpenAI API load or network issues

**Solution**:
- Wait patiently (usually 10-30 seconds)
- Check internet connection
- Try again if it times out

## Related Features

- **Chat Streaming**: Real-time image preview as it generates
- **File Explorer**: Navigate to saved images
- **Background Tasks**: Generate images without blocking workflow

---

**Previous**: [Interactive Questions](./interactive-questions)

**Next**: [Prompt Engineering](../03-advanced-techniques/prompt-engineering)
