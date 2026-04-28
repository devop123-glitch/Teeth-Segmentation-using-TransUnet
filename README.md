# Teeth-Segmentation-using-TransUnet
📌 Overview

This project focuses on automatic teeth segmentation from dental images using a deep learning model based on TransUNet. The goal is to accurately separate teeth regions from the background at the pixel level, which is a fundamental task in medical image analysis.

Segmentation is challenging due to complex tooth structures, low contrast, overlapping boundaries, and imbalance between tooth and background pixels. To address these issues, the model combines convolutional neural networks (CNNs) with transformer-based attention mechanisms.

🧠 Model Architecture (Conceptual Understanding)

The model follows a hybrid encoder–transformer–decoder structure, designed to capture both local details and global context.

🔹 1. Encoder (Feature Extraction using CNN)

The encoder processes the input image through multiple convolutional layers to extract features at different levels.

Early layers capture edges and textures
Deeper layers capture complex structures like tooth shapes
Spatial resolution is gradually reduced while feature richness increases

This stage helps the model understand what is present in the image.

🔹 2. Transformer Module (Global Context Learning)

After feature extraction, the model uses a transformer module to understand relationships across the entire image.

Feature maps are divided into patches and converted into sequences
Positional encoding is added to preserve spatial information
Self-attention mechanism allows the model to focus on relevant regions

Unlike CNNs, which look locally, the transformer captures long-range dependencies, helping distinguish between closely spaced or overlapping teeth.

🔹 3. Decoder (Segmentation Reconstruction)

The decoder reconstructs the segmentation mask from encoded features.

Uses upsampling to restore original image resolution
Combines encoder features through skip connections
Refines boundaries and preserves fine details

This stage determines where each tooth pixel is located.

🔹 4. Output Layer

The final layer produces a binary segmentation mask, where:

Pixel value 1 → Tooth
Pixel value 0 → Background

A sigmoid activation ensures outputs are interpreted as probabilities.

⚖️ Handling Class Imbalance

In dental images, background pixels dominate over tooth pixels. To address this imbalance:

🔸 Focal Loss
Focuses more on difficult or misclassified pixels
Reduces the impact of easy background predictions
🔸 Dice Loss
Measures overlap between predicted and true segmentation
Encourages accurate shape and boundary prediction
✅ Combined Loss

A hybrid approach is used to balance both region accuracy and difficult pixel learning.

🔄 Data Strategy
📊 Stratified Sampling

Instead of random splitting, the dataset is divided based on the foreground ratio (amount of tooth pixels).
This ensures:

Balanced representation of easy and difficult samples
Better generalization during training
🔄 Data Augmentation

To improve robustness, transformations such as flipping, rotation, and scaling are applied.
This helps the model learn invariance to orientation and positioning changes.

📏 Evaluation Metrics
🔹 Dice Coefficient

Measures how well the predicted mask overlaps with the ground truth.
Higher value indicates better segmentation accuracy.

🔹 Intersection over Union (IoU)

Compares the intersection and union of predicted and actual regions.
Provides a stricter evaluation of segmentation quality.

📊 Error Analysis

The model’s predictions are analyzed using visual error maps:

True Positives → correctly segmented teeth
False Positives → background predicted as teeth
False Negatives → missed tooth regions

This helps identify weaknesses such as:

Boundary errors
Missed small regions
Over-segmentation
🚀 Key Strength of the Model

The main strength of this approach lies in combining:

CNNs → strong local feature extraction
Transformers → powerful global context understanding

This hybrid design allows the model to:

Capture fine tooth details
Handle overlapping structures
Improve segmentation consistency
📌 Applications
Dental X-ray analysis
Tooth detection and segmentation
Orthodontic and implant planning
Medical imaging automation
📌 Conclusion

This project demonstrates that integrating convolutional networks with transformer-based attention significantly improves segmentation performance in complex medical images. The approach effectively addresses challenges like class imbalance, unclear boundaries, and structural variability, making it suitable for real-world dental imaging applications.
