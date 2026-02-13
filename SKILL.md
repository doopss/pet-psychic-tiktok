# Pet Psychic TikTok Carousel Automation

## Overview
Automated 6-slide TikTok carousel generation for Pet Psychic app marketing.

## Input Images (ALWAYS in this order)
**4 images required:**
1. `01_pet.jpg` — Pet photo (the star of the show)
2. `02_app_loading.jpg` — App loading screen
3. `03_share_card.jpg` — Share card from app
4. `04_full_reading.jpg` — Full reading result

## Output Slides (6 total)
| Slide | Image Source | Text Overlay |
|-------|--------------|--------------|
| 1 | 01_pet.jpg | Hook: "My boyfriend said pet psychics were fake..." |
| 2 | 01_pet.jpg | Setup: "So I uploaded [Pet Name]'s photo to test it..." |
| 3 | 02_app_loading.jpg | App context text |
| 4 | 03_share_card.jpg | Transition text |
| 5 | 04_full_reading.jpg | Reading highlight |
| 6 | 01_pet.jpg | CTA: "What would YOUR pet say? 🔮 Link in bio" |

## Folder Structure (Auto-Increment)
```
Pet Psychic Automations/
├── Carousel 001/
│   ├── Input/
│   │   ├── 01_pet.jpg
│   │   ├── 02_app_loading.jpg
│   │   ├── 03_share_card.jpg
│   │   └── 04_full_reading.jpg
│   └── Output/
│       ├── slide_01.png
│       ├── slide_02.png
│       ├── slide_03.png
│       ├── slide_04.png
│       ├── slide_05.png
│       └── slide_06.png
├── Carousel 002/
│   └── ...
```

## Auto-Increment Rule
- Check existing carousel folders in Pet Psychic Automations
- Find highest number (e.g., Carousel 001, Carousel 002)
- Increment by 1 for new carousel (003, 004, etc.)
- Always use 3-digit format (001, 002, 010, 100)

## Critical Rules

### 1. Input Image Handling
- **ALWAYS expect 4 images in numbered order**
- Rename to 01_pet.jpg, 02_app_loading.jpg, 03_share_card.jpg, 04_full_reading.jpg
- Upload all 4 to Google Drive Input folder
- Use EXACT images — DO NOT regenerate with AI

### 2. Text Overlay Generation
- **ALWAYS use OpenAI image generation** (gpt-image-1 or DALL-E 3)
- Composite input images with generated backgrounds
- Add text overlays programmatically

### 3. Image Resizing & Fitting (CRITICAL)
**Different rules per slide type:**

**Slides 1, 2, 3, 6 (Pet photos & App loading):**
- Use `Image.Resampling.LANCZOS` for high-quality resize
- Resize to fill entire 1024x1536 canvas
- These images can fill the screen without letterboxing
- **NEVER crop the original image content**

**Slides 4 & 5 (Share card & Full reading):**
- Use `Image.Resampling.LANCZOS` for high-quality resize
- Resize to fit WITHIN 1024x1536 bounds (maintain aspect ratio)
- Add dark navy background (#0F172A) and center the image
- Use letterboxing if needed to prevent cropping
- **NEVER crop the original image content**
- Ensure ALL text is visible, including first/last words and top/bottom content

**Correct approach for slides 4 & 5:**
```python
# Resize to fit within bounds, then paste on dark background
img.thumbnail((1024, 1536), Image.Resampling.LANCZOS)
background = Image.new('RGB', (1024, 1536), (15, 23, 42))  # dark navy
paste_x = (1024 - img.width) // 2
paste_y = (1536 - img.height) // 2
background.paste(img, (paste_x, paste_y))
```

### 5. Text Consistency (CRITICAL)
**ALL text overlays must use EXACT same formatting:**
- **Font:** Same sans-serif font family across ALL 6 slides (Helvetica/Arial)
- **Size:** Same font size (52pt) across ALL 6 slides
- **Position:** Same Y-coordinate (1100, ~72% from top) across ALL 6 slides
- **Format:** Black rounded rectangle highlight with white text
- **Alignment:** Centered horizontally
- **Style:** Bold weight for readability

**Use code to enforce consistency:**
```python
FONT_SIZE = 52
TEXT_Y_POSITION = 300  # Middle of 1536
FONT_NAME = "Helvetica-Bold.ttf"  # or Arial

# Black highlight with rounded corners - EXTRA PADDING to prevent text cut-off
overlay = Image.new('RGBA', img.size, (0,0,0,0))
overlay_draw = ImageDraw.Draw(overlay)
overlay_draw.rounded_rectangle(
    [x-20, y-15, x+text_width+20, y+text_height+15], 
    radius=12, 
    fill=(0,0,0,160)  # semi-transparent black
)
img = Image.alpha_composite(img.convert('RGBA'), overlay).convert('RGB')
# Then add white text
```

### 6. Slide Text Formulas

**Slide 1 — Hook:**
- Pet photo + "My boyfriend said pet psychics were fake..."
- **TEXT FORMAT:** Black rounded highlight + white text

**Slide 2 — Setup:**
- Pet photo + "I uploaded [Pet Name]'s photo to test it" (max 45 characters)
- **TEXT FORMAT:** Black rounded highlight + white text

**Slide 3 — App (BUILD EXCITEMENT):**
- App loading screenshot + "Wait for it..."
- **TEXT FORMAT:** Black rounded highlight + white text
- **Purpose:** Create anticipation/tension

**Slide 4 — Share Card (SIMPLE REVEAL):**
- Share card image RESIZED TO FIT (no cropping)
- Minimal text: "And then..." or "The results:"
- **TEXT FORMAT:** Black rounded highlight + white text
- **Purpose:** Let the share card be the focus, not the overlay text
- **CRITICAL:** Ensure first and last words of share card text are fully visible
- Use letterboxing if needed to preserve entire card content

**Slide 5 — Full Reading (COMMENT, NOT REPEAT):**
- Full reading screenshot RESIZED TO FIT (no cropping)
- Short REACTION/COMMENT on the reading (NOT repeating the reading text)
- Examples: "The accuracy", "How did it know?!", "I'm convinced", "This is too real"
- **TEXT FORMAT:** Black rounded highlight + white text
- **Purpose:** Add human reaction, not duplicate content
- **CRITICAL:** Ensure top and bottom of reading are NOT cut off
- All reading text must be fully visible and readable

**Slide 6 — CTA:**
- Pet photo + "What would YOUR pet say?"
- **TEXT FORMAT:** Black rounded highlight + white text

## Output Requirements
- Save 6 PNGs to: `Pet Psychic Automations/Carousel XXX/Output/`
- Format: PNG, 1024x1536 (TikTok portrait)
- Also upload copy to Google Drive Output folder

## Workflow
1. Find next available carousel number (auto-increment)
2. Create folder structure in Google Drive
3. Receive 4 images, rename to 01_, 02_, 03_, 04_
4. **ALWAYS upload input images to Input/ folder**
5. Generate 6 slides using OpenAI image generation
6. Apply text overlays with correct positioning (higher, centered, serif)
7. Save to local Output/ folder
8. **ALWAYS upload output images to Output/ folder**
9. Report file locations

## Image Naming Convention
When user sends images, ALWAYS rename to:
- First image → 01_pet.jpg
- Second image → 02_app_loading.jpg
- Third image → 03_share_card.jpg
- Fourth image → 04_full_reading.jpg
