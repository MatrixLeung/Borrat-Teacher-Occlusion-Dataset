# Borrat Teacher-Occlusion Dataset

Classroom images with instructor-body masks for teacher detection in lecture scenes.

This dataset accompanies:

> Liang, Z., & Wei, Z. (2026). Borrat: An Infrastructure for Blackboard Occlusion Removal and Restoration for AI Tutoring. In *Proceedings of the 34th International Conference on Computers in Education (ICCE 2026)*. Asia-Pacific Society for Computers in Education.

<p align="center">
  <img src="assets/teaser.jpg" alt="Sample images with instructor masks" width="100%">
</p>

## Dataset

| Split | Images |
|-------|--------|
| train | 320 |
| valid | 80 |
| **total** | **400** |

- Images: JPEG, 1024 × 1024
- Labels: COCO instance segmentation
- Class: `human` (`category_id = 1`), the instructor
- Official split: **train / valid = 320 / 80**

## Layout

```
Borrat-Teacher-Occlusion-Dataset/
  README.md
  LICENSE
  CITATION.cff
  assets/
    teaser.jpg
  train/
    *.jpg
    _annotations.coco.json
  valid/
    *.jpg
    _annotations.coco.json
```

## Annotation format

Each split has a COCO JSON file (`_annotations.coco.json`) with `info`, `licenses`, `categories`, `images`, and `annotations`.

Image record:

```json
{
  "id": 230,
  "file_name": "material-36-_png.rf.fd7bd1d2df0d00649dd0d1a1ec238990.jpg",
  "width": 1024,
  "height": 1024,
  "license": 1,
  "extra": { "name": "material-36-.png" }
}
```

`extra.name` is the source-frame identifier. Images that share the same `extra.name` belong to the same source and are kept in the same split.

Annotation record (`bbox` is `[x, y, width, height]`):

```json
{
  "id": 235,
  "image_id": 230,
  "category_id": 1,
  "bbox": [460.63, 338.17, 261.39, 442.33],
  "area": 115620.639,
  "iscrowd": 0,
  "segmentation": { "counts": "...", "size": [1024, 1024] }
}
```

`segmentation` is COCO RLE or a polygon list. The image file for a record is `<split>/<file_name>`.

## Usage

```python
import json
from pathlib import Path

root = Path("Borrat-Teacher-Occlusion-Dataset")
train = json.loads((root / "train/_annotations.coco.json").read_text())
valid = json.loads((root / "valid/_annotations.coco.json").read_text())

# image path: root / split / image["file_name"]
```

The JSON can also be loaded with `pycocotools.coco.COCO`.

## License

[CC BY 4.0](LICENSE). Please cite the paper if you use this dataset.

## Citation

```bibtex
@inproceedings{liang2026borrat,
  title     = {Borrat: An Infrastructure for Blackboard Occlusion Removal and Restoration for {AI} Tutoring},
  author    = {Liang, Zhanhua and Wei, Zhengyuan},
  booktitle = {Proceedings of the 34th International Conference on Computers in Education},
  year      = {2026},
  publisher = {Asia-Pacific Society for Computers in Education}
}
```
