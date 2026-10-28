# AnEmptySeat

Indoor congestion analysis with YOLOv8m head detection, OC-SORT tracking, and a Django dashboard.

![Supermarket CCTV frame with head boxes, tracking trails, and the overlay "9 people | Status: Common"](docs/assets/result-frame.jpg)

<sub>A frame from the bundled processed video, [`results/supermaket.mp4`](results/supermaket.mp4).</sub>

AnEmptySeat analyzes local MP4 videos to show tracked head counts, crowding levels, and congestion history in the browser.

The bundled head-detection model records **mAP50 0.9247** on `crowd-ah` ([metrics](models/capdi-y8m-640-crowdah-v1-fp32-pt-20250609.metrics.json); the evaluation split is not recorded there). The model metadata links to `KNUT-Capston-DongJunSu/yolo-dev`; the training workspace is also published as [yolov8-head-detection](https://github.com/jwhitekim/yolov8-head-detection).

## Getting Started

Follow the Linux / Ubuntu dependency setup in the [execution guide](docs/README.md) for a Python 3.10 CPU environment.

With that environment active, configure `SECRET_KEY` as described in the guide, keep the bundled models in `models/`, and place a local `.mp4` in `frontend/static/video/` (create the folder if needed).

From the repository root:

```bash
python manage.py runserver
```

Open http://127.0.0.1:8000 and select your video to view its dashboard.

## Further Reading

- [Setup, deployment, and troubleshooting guide](docs/README.md) (Korean)

## Acknowledgements

Built with Ultralytics YOLOv8 and OC-SORT; dataset from AI-Hub. Capstone Design 2025, Department of Electronic Engineering, KNUT — Team DongJunSu (Kim Dong-in, Kim Jun-hee), advised by Prof. Song Chang-ik.

## License

No LICENSE file; license terms need confirmation.
