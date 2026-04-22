# FAQ

**What is EquiLens?**
A system that predicts ML model reliability failures before they occur,
using only the model's prediction outputs.

**What does it need access to?**
Only prediction outputs — confidence scores and class probabilities.
No model weights, training data, or internal representations.

**What models does it work with?**
Any classifier that outputs probabilities: text, image, tabular.
Binary, multi-class, multi-label.

**How is this different from existing monitoring tools?**
Existing tools detect problems after they occur. EquiLens forecasts them in advance.
Existing tools often require model internals. EquiLens requires only outputs.

**Is this open source?**
The research and results are public under CC BY-NC 4.0.
The core system is under active development. Updates coming.

**Where can I follow progress?**
Watch this repo. Read the writing in `writing/`. Paper forthcoming.
