 Conversation opened. 2 messages. All messages read.

Skip to content
Using Gmail with screen readers
3 of 2,887
hii
Inbox

Agarshal
Attachments
9:25 AM (34 minutes ago)
 

Kirthick Kumar <kirthickkumarnj15@gmail.com>
Attachments
9:32 AM (27 minutes ago)
to Abinaya



---------- Forwarded message ---------
From: Agarshal <agarshalgaming@gmail.com>
Date: Wed, Feb 18, 2026 at 9:25 AM
Subject: hii
To: Kirthick Kumar <kirthickkumarnj15@gmail.com>, Akalya <akalyaganesan2006@gmail.com>




 4 Attachments
  •  Scanned by Gmail
import cv2
import numpy as np

# Function to perform motion analysis using moving edges
def motion_analysis(video_path):
    cap = cv2.VideoCapture(video_path)

    # Read the first frame
    ret, prev_frame = cap.read()
    prev_gray = cv2.cvtColor(prev_frame, cv2.COLOR_BGR2GRAY)

    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break

        # Convert the current frame to grayscale
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

        # Perform Canny edge detection on both frames
        edges_prev = cv2.Canny(prev_gray, 50, 150)
        edges_curr = cv2.Canny(gray, 50, 150)

        # Compute frame difference to detect moving edges
        frame_diff = cv2.absdiff(edges_prev, edges_curr)

        # Display the moving edges
        cv2.imshow('Moving Edges', frame_diff)
        if cv2.waitKey(30) & 0xFF == ord('q'):
            break

        # Update the previous frame and previous grayscale image
        prev_gray = gray.copy()

    cap.release()
    cv2.destroyAllWindows()


# Replace 'path_to_video.mp4' with your video file path
video_path = "video.mp4"
motion_analysis(video_path)
program5.py
Displaying detect.py.




https://github.com/user-attachments/assets/45c8a7fe-b490-4521-af86-0db4b6c282d2

