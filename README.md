<p align="center">
  <img src="assets/icon.svg" alt="redacTUM icon" width="120">
</p>

# redacTUM

Blacks out the exam identifiers on scanned TUM exam/assignment PDFs so they can be shared without revealing which exam booklet they belong to.

Built to anonymize exam scans before they are shared for tutorials, exam reviews, second examiners or didactics research, in line with GDPR data minimization.

> **Disclaimer:** For educational purposes only. redacTUM does not endorse distributing exams in violation of anyone's copyright.
>
> This is an independent project. It is not affiliated with, endorsed by, or in any way official to the Technical University of Munich (TUM). The name is just a pun.

## What it does

1. Finds and covers with black boxes:
   - the full exam ID (`YYYY-NN-NNNN-ENNNN-NN`) in the footer and rotated along the page edge,
   - the short booklet/pseudonym ID (`ENNNN`) in the sticker box on page 1,
   - the Data Matrix codes in the page corners (sorry, little robots).
2. Rasterizes every page (300 DPI by default) into a new image-only PDF, so the covered text cannot be recovered from the text layer.
3. Strips the document metadata.

The output has no selectable text. The detection is tuned to the TUM exam layout. Check the result before sharing it.

## Prerequisites

- Python 3.9+
- [Poppler](https://poppler.freedesktop.org/) (`pdftoppm`)
- Python packages: `pdfplumber`, `pypdf`, `reportlab`
- An exam you are allowed to share. Allegedly.

```bash
brew install poppler            # macOS; on Debian/Ubuntu: apt install poppler-utils
pip install -r requirements.txt
```

## Usage

```bash
python3 redactum.py INPUT.pdf OUTPUT.pdf [DPI]
```

Example:

```bash
python3 redactum.py exam_scan.pdf exam_scan_redacted.pdf 200
```

The script reports how many regions it covered on each page. Input and output must be different files.

## License

[GPL-3.0](LICENSE). The exams themselves are not covered by this license. Obviously. 👀

<!-- You found the raw markdown. Sadly, the solutions aren't in here either. -->
