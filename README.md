# Golf Swing Phase Detection & Comparison

A computer vision tool that analyzes golf swing videos using MediaPipe Pose. It automatically detects key swing phases and compares a player's swing against a professional reference swing.

The system extracts wrist movement throughout the swing, segments motion into golf-specific phases, and generates coaching feedback based on body mechanics such as shoulder-hip separation, arm extension, hand position, and spine posture.

---

# Features

## Automatic Swing Phase Detection

Using wrist trajectory data extracted from MediaPipe Pose landmarks, the system automatically identifies:

- Address  
- Backswing  
- Top of Backswing  
- Downswing  
- Impact  
- Follow Through  

No manual frame labeling is required.

---

## Pose-Based Swing Comparison

For each detected phase, the system compares a golfer's swing against a professional reference swing and evaluates:

- Arm extension  
- Hand height  
- Spine tilt  
- Shoulder-hip separation (X-Factor)  

---

## Coaching Feedback Generation

Differences between the player and professional swing are converted into actionable coaching advice.

Each issue includes:

- Why it matters  
- Suggested drill  
- Swing phase context  

### Example Issues

- Over-rotating shoulders relative to hips  
- Hands too high at address  
- Arms excessively extended  
- Insufficient shoulder-hip separation during transition  

---

# How It Works

## 1. Pose Extraction

MediaPipe Pose is used to detect body landmarks in every frame.

For each frame, the system extracts:

- Left wrist position  
- Right wrist position  
- Wrist visibility confidence  

The average wrist height is used as the primary motion signal.

---

## 2. Swing Detection

The wrist trajectory is smoothed and differentiated to calculate motion velocity.

The algorithm determines:

- Swing start  
- Top of backswing  
- Impact  
- Follow through  

These are derived from changes in wrist movement over time.

---

## 3. Phase Segmentation

Detected motion is split into:

- Address  
- Backswing  
- Top  
- Downswing  
- Impact  
- Follow Through  

Each phase is represented as a frame range.

### Example

```json
{
  "Address": [0, 24],
  "Backswing": [24, 71],
  "Top": [71, 81],
  "Downswing": [81, 103],
  "Impact": [103, 108],
  "Follow Through": [108, 145]
}
