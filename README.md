
## LicencePlateRegconition

Professional summary
--------------------

LicencePlateRegconition is a production‑oriented, two‑stage license‑plate recognition system I designed and implemented end‑to‑end. The pipeline uses a high‑quality object detector for robust plate localization followed by a sequence recognizer for accurate transcription. I was responsible for dataset collection and VOC annotation, model design and training, inference pipeline engineering, and empirical evaluation.

Key highlights
--------------

- Two‑stage architecture: Faster R‑CNN (ResNet‑50 FPN) for detection + CRNN (CNN→sequence head) for recognition. 
- Practical engineering: VOC XML → JSON conversion, deterministic preprocessing for inference, and a Tesseract fallback for edge cases.
- Reproducible notebooks: `train_plate.ipynb` (detection) and `train_char.ipynb` (recognition) include data preparation, model code and training loops.

Compact results
---------------

| Method | Precision | Recall | Time per image | Confidence on same labeled object |
|---|---:|---:|---:|---:|
| Faster R‑CNN | 93.5% | 92.3% | 2.4 s | 0.9 → ~1 |
| YOLOv7 | 92.4% | 91.1% | 1.7 s | 0.7 → ~0.9 |

Quickstart (local)
------------------

1. Create and activate a Python 3.8+ environment.

```powershell
pip install -r requirements.txt
jupyter notebook "train_plate.ipynb"
```

2. Update dataset paths in the notebooks (the development notebooks contain absolute paths such as `D:\\data_cpv\\...`).
3. Run `train_plate.ipynb` to prepare annotations and train the detector. Use the produced checkpoint to generate plate crops.
4. Prepare the character dataset from the crops and run `train_char.ipynb` to train the CRNN recognizer.

Reproducibility notes
---------------------

- Checkpoints and expected artifacts: `dataset.json`, `train2/fasterrcnn_resnet50_fpn_epoch_*.pth`, `char_trained_models/character_recognition_crnn_epoch_*.pth`, `result/`, `cropped/`.
- Tesseract: install the Tesseract binary for OCR fallback and set `pytesseract.pytesseract.tesseract_cmd` to the exe path on Windows.
- If you plan to run training on GPU, ensure appropriate CUDA and PyTorch builds are installed.

Structure
---------

- `train_plate.ipynb` — dataset conversion (VOC XML), `LicensePlateDataset`, Faster R‑CNN model setup, training loop and inference example with cropping and Tesseract postprocessing.
- `train_char.ipynb` — character dataset loader (folder-per-class), CRNN model, CTC training loop and checkpointing.
- `Paper.pdf` — project paper describing methodology and evaluation (kept in workspace). For verbatim metrics or tables, extract the paper text and add to documentation.

Contact & reuse
---------------

If you reuse code or data, please credit the project author and respect any dataset usage constraints. For questions or to request evaluation artifacts (full metrics, trained checkpoints), open an issue or contact the project owner.

License
-------

This repository and its notebooks are provided by the project author; include an appropriate license when publishing or sharing derived work.
