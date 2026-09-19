# Add your assets here

These optional filenames are recognized automatically:

- `game.pdf`: graph/game illustration
- `hardness.pdf`: reduction illustration
- `algorithm.pdf`: tree partition/interface illustration
- `hvl-logo.pdf`: institutional logo
- `game-qr.pdf`: QR code for the browser demo (generated for this project)
- `game-qr.svg`: the same QR code as an editable vector asset

PDF is recommended for graph figures so that text and lines remain sharp.
To use another filename or a PNG/JPEG, edit the matching file in `figures/`.
The logo path is set in `config.tex`.

The QR code opens `https://thobiashoivik.com/lab/geography-playground` and is
placed by `content/demo.tex`. Replace the generated files only if the demo URL
changes; keep a quiet white border around the code when editing it.

When an asset is missing, the project compiles with a placeholder of the same
height. No external images or logo are required to compile this starter.
