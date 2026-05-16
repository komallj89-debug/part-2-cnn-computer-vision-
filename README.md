# Part 2: Computer Vision Problem Formulation and CNN Prototype

This repository contains an end-to-end Computer Vision project using a Convolutional Neural Network (CNN) built with TensorFlow and Keras.

---

##  Repository Layout Structure
* **`README.md`**: This document containing comprehensive project descriptions and concept answers.
* **`notebook.ipynb`**: The interactive Jupyter/Google Colab notebook executing the code pipeline.
* **`requirements.txt`**: Plain text file listing all necessary library versions for runtime environment replication.
* **`results/accuracy_loss_curves.png`**: Visual training history tracing model improvement across learning epochs.
* **`results/confusion_matrix.png`**: Evaluation matrix map comparing actual categories against AI predictions.
* **`sample_predictions/prediction_outputs.png`**: Visual display mapping predictions directly on unseen sample images.

---

##  Task 1: Problem Identification
* **Problem Type Selected:** Image Classification.
* **Core Objective:** The dataset requires taking a whole input image and matching it to a single categorical label.
* **Why Object Detection is incorrect:** The task does not require tracing specific location boxes (`bounding boxes`) around separate components inside the photo.
* **Why Segmentation is incorrect:** The model does not need to analyze or color boundaries down to the pixel level.
* **Conclusion:** Because the task treats each input photograph as a single target to categorize into discrete structural slots, Image Classification is the appropriate choice.

---

##  Task 2 & 3: Dataset Exploration & Preprocessing
* **Total Image Count:** 480 total images extracted from the provided archive file.
* **Training Partition Size:** 384 images (80%) used directly by the network to optimize weights.
* **Testing/Validation Partition Size:** 96 images (20%) entirely withheld to evaluate out-of-sample performance.
* **Image Dimensions:** Uniformly scaled to $128 \times 128$ dimensions using 3 color channels (RGB).
* **Dataset Balance State:** Balanced configuration across training streams, avoiding learning skews or majorities.
* **Applied Image Preprocessing Pipeline:**
  * **Automated Extraction:** Programmatically unzips the uploaded archive directly into the working directory.
  * **Uniform Resizing:** Forces various raw picture dimensions into a consistent $128 \times 128$ pixel grid.
  * **Pixel Value Normalization:** Scales raw color numbers down from $[0, 255]$ to a stable $[0.0, 1.0]$ floating-point spectrum to accelerate model convergence.
  * **Real-time Data Augmentation:** Deploys shifts, rotations, zoom limits, and horizontal mirroring on training batches to prevent overfitting.

---

##  Task 4 & 5: CNN Model Design and Evaluation
* **Convolution Layers (`Conv2D`):** Scans 2D pixel layouts using mathematical filters to discover visual micro-features like lines and borders.
* **Activation Functions (`ReLU`):** Drops negative intermediate math results to zero to give the network non-linear pattern learning capabilities.
* **Pooling Layers (`MaxPooling2D`):** Slides downsampling matrices over feature maps, keeping only the maximum values to shrink data volume.
* **Flatten Layer:** Unrolls multidimensional matrices into a single row of continuous numeric strings.
* **Dense (Fully Connected) Classifier:** Integrates hidden layers with a $50\%$ Dropout protection filter to translate textures into real class scores.
* **Output Activation (`Sigmoid`):** Maps results to a clear mathematical probability boundary between 0 and 1.
* **Performance Logs:** Tracked in the `results/` charts, showing smooth loss reductions and accurate tracking across test groups.

---

##  Task 6: CNN Core Theoretical Explanations
* **What is Convolution?**
  * It is a scanning operation where a small grid of numbers (called a filter or kernel) moves pixel-by-pixel across an image.
  * At each step, it multiplies its numbers by the pixel values it covers to create a feature map.
  * This mathematical filtering enables the network to notice crucial visual indicators like sharp borders, lines, and textures.
* **Why is Pooling Used?**
  * Images contain massive amounts of redundant spatial details that slow down computer calculations.
  * Pooling layers systematically shrink the height and width of image representations by keeping only the most important values (like the highest number in a $2 \times 2$ grid).
  * This speeds up training time, saves computer memory, and helps the model recognize shapes even if they shift or rotate slightly.
* **Why is ReLU (Rectified Linear Activation) Commonly Used?**
  * The formula is extremely simple: $f(x) = \max(0, x)$, converting all negative numerical inputs to zero while passing positive values as-is.
  * This basic calculation introduces the necessary non-linearity to let networks map intricate real-world textures.
  * It fixes the "vanishing gradient" problem—a mathematical stall that causes older deep networks to stop learning entirely during training.
* **Why are CNNs Better than Regular Feed-Forward Networks for Image Data?**
  * Regular feed-forward networks require an image to be unrolled into a flat row of numbers, destroying spatial relationships (the network forgets that eyes sit near a nose).
  * CNNs preserve 2D and 3D geometric relationships by processing pixels in clusters.
  * CNNs utilize **parameter sharing**, meaning a filter that learns to find a texture pattern in the top corner of a photo can instantly recognize that same pattern anywhere else.

---

##  Task 7: Business Use Case Mapping
* **Selected Domain:** Manufacturing & Industrial Automation.
* **The Operational Problem:** Traditional visual quality control on assembly lines relies on human inspectors, which introduces issues with fatigue, high labor costs, and varied accuracy across long shifts.
* **The CNN Solution:** Automated camera structures record components on active conveyor tracks, passing them straight to this trained CNN classification model to automatically flag items as `Normal` or `Defective`.
* **Cost Optimization:** Lowers continuous operational overhead and manual screening expenses via automation.
* **Risk Mitigation:** Drops error margins down significantly, blocking defective components before they leave the factory floor to safeguard brand reputation.
* **Predictive Maintenance Insights:** Gives manufacturing managers data to notice sudden spikes in particular defect types, allowing them to fix faulty machinery before it breaks.
