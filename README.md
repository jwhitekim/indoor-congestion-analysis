# AnEmptySeat

Indoor congestion analysis with YOLOv8m head detection, OC-SORT tracking, and a Django dashboard.

![Supermarket CCTV frame with head boxes, tracking trails, and the overlay "9 people | Status: Common"](docs/assets/result-frame.jpg)

<sub>A frame from the bundled processed video, [`results/supermaket.mp4`](results/supermaket.mp4).</sub>

AnEmptySeat reads local MP4 videos and reports head counts and crowding levels. Its congestion score combines the head count with the mean distance between tracked heads, so a tight cluster scores higher than the same number of people spread across the frame.

The bundled head-detection model records **mAP50 0.9247** on `crowd-ah` ([metrics](models/capdi-y8m-640-crowdah-v1-fp32-pt-20250609.metrics.json); the evaluation split is not recorded there). The model metadata links to `KNUT-Capston-DongJunSu/yolo-dev`; the training workspace is also published as [yolov8-head-detection](https://github.com/jwhitekim/yolov8-head-detection).

## Features

- Head detection and ID tracking across frames
- Four congestion levels from a smoothed score: Normal, Common, Crowded, Very Crowded
- Live annotated video (MJPEG), current counts, and congestion history in the browser
- Short-term congestion forecast from recent counts with a saved regression model

## Getting Started

Set up Python 3.10 and the dependencies with the [Windows/Linux setup guide](docs/README.md). Note that `requirements.txt` is missing some packages the app uses (`matplotlib`, `scikit-learn`, `lap`/`lapx`).

1. Put `SECRET_KEY` in a root `.env` file.
2. Keep the bundled models in [`models/`](models/) (file names are set in [`settings.py`](backend/config/settings.py)).
3. Create `frontend/static/video/` and put your `.mp4` files there.

```bash
python manage.py runserver
```

Open http://127.0.0.1:8000, pick a video, and its dashboard opens.

## Limitations

- Input is local video files only.
- Scores use image-space distances and fixed thresholds, so camera angle and occlusion affect them.
- The training-data generator samples about once per second, while the app collects one sample per processed frame; forecast horizons need validation.

## Further Reading

- [Setup, deployment, troubleshooting](docs/README.md) — its script examples use older root-level paths; scripts now live in [`scripts/`](scripts/)
- [Congestion score](backend/videostream/analytics/occupancy.py) · [Level classification](backend/videostream/analytics/calc_congestion.py)

## Acknowledgements

Built with Ultralytics YOLOv8 and OC-SORT; dataset from AI-Hub. Capstone Design 2025, Department of Electronic Engineering, KNUT — Team DongJunSu (Kim Dong-in, Kim Jun-hee), advised by Prof. Song Chang-ik.

## License

No LICENSE file; license terms need confirmation.
