# Ayna-project
# Polygon Colorization with Conditional UNet

This project trains a UNet model to colorize a given polygon image based on a specified color name. The goal is to produce a realistic, colored polygon as output, conditioned on the input image (outline) and a target color.

## 🚀 Assignment Details

- **Input:** Grayscale image of a polygon, plus a color name (`"blue"`, `"yellow"`, etc.)
- **Output:** Colored (RGB) polygon image matching the input shape and color
- **Dataset:** Provided by Ayna (see structure below)
- **Model:** PyTorch UNet, conditioning via learned color embeddings
- **Experiment Tracking:** [Weights & Biases](https://wandb.ai/) (see project link below)
- **Validation:** Performance evaluated visually and by loss on validation set


---

## 🏗️ Model Architecture

- **Base:** Standard U-Net
- **Conditioning:** Color name is mapped to an integer, then embedded and concatenated as extra channels to each input image
- **Input:** (`1+embedding_dim`, 128, 128) tensor
- **Output:** (3, 128, 128) tensor (RGB image)

### UNet Block (condensed):

- **Encoder:** Double conv blocks, max pool
- **Bottleneck:** Deepest feature map
- **Decoder:** Transposed conv, skip connections, double conv blocks
- **Output:** 3-channel RGB image

---

## 🏃 Training Strategy

- **Loss:** MSE (Mean Squared Error) over RGB pixels
- **Optimizer:** Adam, `lr=1e-3`
- **Epochs:** 10—20 (could increase for best results)
- **Batch size:** 8
- **Hardware:** Colab (T4/P100 GPU)

All training runs, hyperparams, and curves logged to [Weights & Biases](https://wandb.ai/kasivisweswarreddy6-bharath-university/aynapolygon).

---

## 🧩 How To Run

1. **Clone repo & install requirements:**
    ```
    pip install torch torchvision wandb
    ```
2. **Get the data.**  
   Download or extract the dataset into the root directory, matching the structure above.
3. **Train the model:**
   Open `notebook.ipynb` in Colab or locally and run the cells.
4. **Run inference:**  
   Use the sample code at the end of the notebook to visualize predictions.

---

## 📊 Results & Insights

- **Training loss** dropped from ~1.01 to ~0.10 (MSE) in 10+ epochs.
- **Outputs:** Generated colored polygons match requested colors and target shapes with high fidelity.
- **Failure modes:** Minor confusion on visually similar colors/shapes; can be minimized with more data augmentation.
- **Key learnings:**
    - Early embedding conditioning is simple, robust, and effective for this task.
    - Logging qualitative examples to wandb is invaluable for debugging.


---

## 🤖 Author

Ayna ML Assignment — Kasivisweswar Reddy, 2025
