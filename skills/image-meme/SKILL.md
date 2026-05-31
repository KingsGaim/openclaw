---
name: image-meme
description: "Create memes, edit images, and generate visual content with PIL, canvas, and meme-maker tools."
---

# Image & Meme Tools

Create memes, edit images, and generate visual content.

## Available Skills

### meme-maker
Location: `~/.nvm/versions/node/v24.14.0/lib/node_modules/openclaw/skills/meme-maker/SKILL.md`

Generate meme images from templates or custom images.

### canvas
Location: `~/.nvm/versions/node/v24.14.0/lib/node_modules/openclaw/skills/canvas/SKILL.md`

Draw custom graphics, charts, diagrams, and illustrations.

### diagram-maker
Location: `~/.nvm/versions/node/v24.14.0/lib/node_modules/openclaw/skills/diagram-maker/SKILL.md`

Create flowcharts, architecture diagrams, sequence diagrams.

## PIL Image Operations

```python
from PIL import Image, ImageDraw, ImageFont

# Create image
img = Image.new('RGB', (800, 600), 'white')
draw = ImageDraw.Draw(img)

# Draw shapes
draw.rectangle([50, 50, 200, 200], fill='blue', outline='black')
draw.ellipse([250, 50, 400, 200], fill='red')
draw.line([(0, 0), (800, 600)], fill='black', width=2)

# Add text
font = ImageFont.truetype('/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf', 24)
draw.text((50, 250), 'Hello World', fill='black', font=font)

# Overlay text on image
base = Image.open('base.jpg').convert('RGBA')
txt = Image.new('RGBA', base.size, (255, 255, 255, 0))
draw = ImageDraw.Draw(txt)
draw.text((50, 50), 'Meme Text', fill=(255, 255, 255, 200), font=font)
out = Image.alpha_composite(base, txt)

# Save
img.save('output.png')
```

## Chinese Font Support

Common paths:
- Linux: `/usr/share/fonts/truetype/wqy/wqy-zenhei.ttc`
- Or install: `apt-get install fonts-wqy-zenhei`

## Meme Patterns

1. Find template image
2. Load with PIL
3. Add text overlay at calculated positions
4. Save and send

## Best Practices

- Use PNG for text-heavy images (sharp edges)
- JPEG for photos (smaller file size)
- Keep meme text large and readable
- Center-align for impact
- Add stroke/outline for readability on any background
