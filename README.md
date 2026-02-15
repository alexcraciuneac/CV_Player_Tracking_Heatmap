# Football Player Tracking & Tactical Analysis

### CV2026 -- Computer Vision Project

This project explores how modern computer vision techniques can be
applied to football match analysis. The goal was to build a practical
pipeline capable of detecting players, identifying teams automatically,
tracking spatial influence on the pitch, and estimating possession using
only video input.

Rather than focusing only on object detection, the project extends into
tactical analytics by combining deep learning with unsupervised
clustering and spatial statistics.

------------------------------------------------------------------------

## What the System Does

The implemented pipeline performs the following steps:

• Detects players using YOLOv8\
• Automatically separates teams based on jersey color (HSV + KMeans)\
• Builds spatial heatmaps for each team\
• Detects the ball and accumulates its trajectory\
• Estimates possession by proximity to the ball\
• Computes pitch dominance between teams\
• Analyzes control across defensive, middle and attacking thirds

All processing is performed directly from broadcast-style match footage.

------------------------------------------------------------------------

## Core Ideas Behind the Approach

### Player Detection

Players are detected frame-by-frame using YOLOv8. Only the "person"
class is kept to isolate football players from background objects.

### Automatic Team Identification

Instead of manually labeling teams, the system extracts HSV features
from each player's jersey region.\
KMeans clustering (k = 2) is then applied to separate players into two
dominant color groups.

### Heatmap Generation

Player positions are accumulated over time.\
Gaussian smoothing is applied to produce continuous spatial influence
maps.\
These are normalized and overlaid on the pitch.

### Possession Estimation

Ball detections are compared against nearby players.\
The closest player determines possession for that frame.\
Statistics are accumulated across the processed sequence.

### Field Dominance

Every pixel on the pitch is assigned to the team with higher accumulated
presence intensity, resulting in a dominance map.

### Tactical Third Analysis

The pitch is divided horizontally into: - Defensive third\
- Middle third\
- Attacking third

Dominance values are computed independently for each zone.

### Ball Trajectory Heatmap

Ball center coordinates are accumulated to generate: - A trajectory
visualization\
- A spatial intensity heatmap

------------------------------------------------------------------------

## Technologies Used

-   Python\
-   OpenCV\
-   NumPy\
-   Matplotlib\
-   Scikit-learn (KMeans)\
-   YOLOv8 (Ultralytics)

------------------------------------------------------------------------

## Example Results

Processed frames: 375\
Ball detections: 242\
Possession distribution: \~56% vs 44%\
Dominance split: \~52% vs 48%

These results demonstrate how spatial control and ball interaction can
be approximated using only computer vision techniques.

------------------------------------------------------------------------

## Academic Context

Master Program: Big Data\
Course: Computer Vision 2026\
Application Domain: Sports Analytics

------------------------------------------------------------------------

## How to Run

1.  Open the notebook in Google Colab\

2.  Install required dependencies:

        pip install ultralytics opencv-python scikit-learn matplotlib

3.  Upload the football video\

4.  Run all cells

------------------------------------------------------------------------

This project represents a practical application of detection, clustering
and spatial analysis techniques in a real-world sports scenario.
