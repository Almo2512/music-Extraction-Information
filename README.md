# Audio Processing and Feature Analysis

This project provides tools for analyzing audio files, extracting low-level features, and mapping these features to color representations. It includes three main components:

1. **Audio Feature Extraction** - Extracting features from audio segments.
2. **Feature Display and Analysis** - Displaying, analyzing, and plotting extracted audio features.
3. **Audio to Color Mapping** - Training a model to map audio features to visual colors and visualizing the results.

---

## Table of Contents

- [1. Audio Feature Extraction](#1-audio-feature-extraction)
- [2. Feature Display and Analysis](#2-feature-display-and-analysis)
- [3. Audio to Color Mapping](#3-audio-to-color-mapping)
- [Dependencies](#dependencies)
- [Usage](#usage)

---

## 1. Audio Feature Extraction

The **AudioFeatureExtractor** class extracts audio features in segments, providing a detailed low-level analysis using the `opensmile` library. The features extracted are based on the eGeMAPS feature set and include statistical measures like mean, standard deviation, max, and min for each feature in each segment.

### Key Components:

- **Segmented Processing:** Audio is divided into 2-second segments (or customizable length), allowing precise timestamped analysis.
- **Feature Extraction:** Each segment's audio features are extracted and saved in JSON format for easy access and subsequent analysis.
- **Data Storage:** The extracted features can be saved to a JSON file for visualization and analysis.

### Code Overview:

- **`load_audio`**: Loads an audio file (WAV or MP3) using `librosa`.
- **`extract_features`**: Extracts features for each segment, saving segment statistics and timestamp data.
- **`save_features`**: Saves the extracted feature data to a specified output file.

### Example Usage:

To extract features from an audio file and save them to a JSON file:

```python
extractor = AudioFeatureExtractor(segment_duration=2.0)
features = extractor.extract_features("audio_file.wav")
extractor.save_features(features, "features.json")
```

---

## 2. Feature Display and Analysis

The feature display component visualizes the extracted features for exploratory data analysis, displaying segment statistics and plotting time-based feature trends.

### Key Components:

- **Display Options:** Provides both a basic JSON view of feature data and a detailed analysis with summary statistics.
- **Data Flattening and Formatting:** For detailed views, data is flattened to a format suitable for analysis in a `pandas` DataFrame.
- **Plotting Feature Trends:** Time-series plots show feature changes over time, allowing insights into how specific characteristics (e.g., loudness, pitch) evolve across the audio.

### Code Overview:

- **`display_features`**: Prints the basic JSON contents of the extracted features.
- **`display_features_detailed`**: Loads the feature data into a DataFrame for a detailed display of statistics and segment counts.
- **`plot_features`**: Plots the means of selected features over time to illustrate trends.

### Example Usage:

To display or plot features from a saved JSON file:

```python
display_features()  # Display basic JSON content
display_features_detailed()  # Display detailed analysis with statistics
plot_features()  # Plot time-series trends of features
```

---

## 3. Audio to Color Mapping

This module trains a neural network to map audio features to colors, representing the audio's mood or energy visually. This mapping model can later be used to assign colors to new audio samples based on their feature patterns.

### Key Components:

- **Feature Preparation:** Extracted features are prepared and normalized for training.
- **Model Training:** A `MLPRegressor` neural network is trained to map features to RGB color values.
- **Color Visualization:** Using `matplotlib`, the resulting colors are visualized as colored spans for each audio segment.

### Code Overview:

- **`prepare_features`**: Prepares audio features from JSON for model input by flattening and normalizing values.
- **`map_features_to_color`**: Maps normalized features to HSV values, then converts them to RGB.
- **`visualize_colors`**: Displays the mapped colors as horizontal bars, providing a visual summary of the audio's dynamic attributes.

### Example Usage:

To train the color mapping model and visualize the resulting colors:

```python
mapper = train_and_visualize()  # Train model and visualize color mapping
```

To map new audio features to colors with a pre-trained model:

```python
new_colors = map_realtime_audio(mapper, new_features)
```

---

## Dependencies

- **Python Libraries**: `opensmile`, `librosa`, `soundfile`, `json`, `numpy`, `pandas`, `matplotlib`, `sklearn`

Install all dependencies:

```bash
pip install opensmile librosa soundfile numpy pandas matplotlib scikit-learn
```

## Usage

1. **Extract Features**: Use `AudioFeatureExtractor` to process an audio file, dividing it into segments and saving features to JSON.
2. **Display/Analyze Features**: Display feature details, summarize statistics, and plot features over time.
3. **Map Features to Colors**: Train the `AudioToColorMapper` model with extracted features, generate colors for new audio data, and visualize results.
