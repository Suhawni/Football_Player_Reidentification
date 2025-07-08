Football Player Tracking & Re-Identification

This project performs player detection, tracking, and Re-identification from a football match video. It processes the input video to assign each player a unique ID and ensures consistent tracking across frames, even after occlusion or motion.

Sample Output
![output_videos\output_image.png](https://github.com/Suhawni/Football_Player_Reidentification/blob/main/output_videos/output_image.png)

Project Structure

football_analysis/

├── input_videos/ # Folder containing input video

│ └── 15sec_input_720p.mp4

├── models/ # Folder storing trained detection model

│ └── best.pt

├── output_videos/ # Output folder with result video

│ └── output.avi

  └──output_image.png
  
├── tracker_stubs/ # Stored detection results for analysis

│ └── player_detection.pkl

├── trackers/ # Re-identification & tracking code

│ ├── init.py

│ └── tracker.py

├── utils/ # Utility functions

  ├──init.py
  
  ├──tracker.py
  
├── main.py # Main entry point to run the pipeline

├── requirements.txt # Python dependencies

└── README.md # Project documentation


How It Works

1. Player Detection  
   YOLOv11 (`best.pt`) is used to detect players, referees, and the ball in each frame.

2. Player Identification & Tracking
   Each detected player is assigned a unique ID. The system uses appearance and motion-based tracking to maintain ID consistency across frames.

3. Re-Identification (Re-ID) 
   When a player disappears and reappears, the system re-identifies them based on features like location and appearance, preventing duplicate IDs.

4. Output Generation 
   A new video (`output.avi`) is generated with bounding boxes and consistent IDs over time.


Installation

1. Clone the repository:
   ```bash
   `git clone https://github.com/yourusername/football_analysis.git`
   `cd football_analysis`
   
2. Install dependencies:
    `pip install -r requirements.txt`

3. To run the complete pipeline on the input video:
    `python main.py`

This will:
1. Process the video from input_videos/15sec_input_720p.mp4

2. Perform detection, tracking, and re-identification

3. Save the final output video to output_videos/output.avi

The output video will show:

1. Detected players and referees

2. Consistent IDs for each player

3. Smooth tracking even after players leave and re-enter the frame

Notes
1. YOLOv11 weights (best.pt) are pre-trained and already provided for football-specific player, referee, and ball detection. No training is required — just run and analyze.

2. player_detection.pkl is a helper artifact that stores frame-wise detection results, including bounding boxes for players, referees, and the ball. This allows you to:

-> Avoid redundant YOLO inference during development or debugging

-> Use consistent detection data for re-identification and visualization

3. Re-Identification (Re-ID) is handled using a combination of IoU (Intersection over Union) and color histogram similarity, ensuring each player is assigned a unique and consistent ID throughout the match, even after disappearing and reappearing in the frame.

