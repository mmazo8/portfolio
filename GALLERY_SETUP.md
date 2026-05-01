# Gallery Setup

## Adding Photos

1. Create a `gallery/` folder in your portfolio root (same level as `index.html`)
2. Drop your photos in — any of these formats work: `.jpg`, `.jpeg`, `.png`, `.webp`, `.gif`, `.avif`

## Creating the Manifest

Because browsers can't read a folder listing directly, you need a small `manifest.json` file that lists your photo filenames. Create `gallery/manifest.json` like this:

```json
[
  "photo1.jpg",
  "photo2.jpg",
  "vacation.png",
  "my-dog.jpg"
]
```

The gallery will load them in the order they appear in the list.

## Quick manifest generator (run from your portfolio root)

If you have Node.js, run this in terminal:

```bash
node -e "
const fs = require('fs');
const exts = ['.jpg','.jpeg','.png','.webp','.gif','.avif'];
const files = fs.readdirSync('./gallery').filter(f => exts.includes(require('path').extname(f).toLowerCase()));
fs.writeFileSync('./gallery/manifest.json', JSON.stringify(files, null, 2));
console.log('manifest.json created with', files.length, 'photos');
"
```

Or with Python:

```bash
python3 -c "
import os, json
exts = {'.jpg','.jpeg','.png','.webp','.gif','.avif'}
files = [f for f in os.listdir('gallery') if os.path.splitext(f)[1].lower() in exts]
files.sort()
json.dump(files, open('gallery/manifest.json','w'), indent=2)
print(f'manifest.json created with {len(files)} photos')
"
```

That's it — refresh the gallery page and your photos will appear!
