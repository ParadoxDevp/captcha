# 🎬 Video CAPTCHA

A human-verification CAPTCHA built on video comprehension. Instead of distorted text or image grids, users watch a short YouTube clip and pick the correct description from 4 options — one real, three from completely different videos.

Traditional CAPTCHAs are increasingly bypassed by AI. Video comprehension requires understanding *what action is happening* over time, not just pattern-matching static images. The cost to automate this at scale rarely justifies the reward.

## Dataset

**MSR-VTT** — Microsoft Research Video to Text (CVPR 2016)
- 10,000 YouTube clips, each with ~20 crowd-sourced captions
- 9,000-clip training split (`msrvtt_train_9k.json`) used here
- Source: [friedrichor/MSR-VTT on HuggingFace](https://huggingface.co/datasets/friedrichor/MSR-VTT)

## How it works

1. The full JSON dataset is fetched on page load
2. A random video clip is embedded (looped between its start and end timestamp)
3. One caption is randomly picked from that video's ~20 annotations as the correct answer
4. Three wrong captions are randomly sampled from other videos
5. User picks the matching description — up to 3 video swaps allowed

## Run locally

```bash
git clone <repo-url>
cd captcha

# Serve over HTTP (required — YouTube embeds don't work on file://)
python3 -m http.server 8765
```

Open **http://localhost:8765**
