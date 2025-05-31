# TalkNet-Speaker-Activity-JSON

This repository provides a **modified version of `demoTalkNet.py`** that adds a post-processing function to generate a structured **JSON file** with **speaker activity segments** and their estimated **position (left/right)**.

---

## ✨ What's New?

I've added a new function called `generate_speaker_activity_json()` which:
- Processes face tracking data and activity scores,
- Identifies when speakers are active,
- Estimates their position (left or right) based on face bounding box centers,
- Saves all detected segments in a clear and structured JSON file.

---

## 🔧 How to Use It

You can follow the **exact same installation and inference steps as the original TalkNet repository**, with one simple change:

### ✅ Steps:

1. **Clone TalkNet** as described in the original [TalkNet-ASD repository](https://github.com/TaoRuijie/TalkNet-ASD).
2. **Replace** their original `demoTalkNet.py` script with the one provided here (in this repository).
3. **Run inference** as usual:
   python demoTalkNet.py --video input_video.mp4
4. After inference, a new JSON file will be generated in your output directory, containing speaker activity segments with timestamps and speaker position.

📝 JSON Format Example
```json
{
  "0": [
    {
      "start": 1.48,
      "end": 4.84,
      "position": "right"
    }
  ],
  "1": [
    {
      "start": 6.12,
      "end": 9.60,
      "position": "left"
    }
  ]
}
```

### 💡 Notes
The speaker position is estimated based on the average center x-coordinate of bounding boxes over the whole track.

Segment smoothing is applied: speakers are considered active after 45 consecutive frames above threshold, and segments end after 30 consecutive frames below.
