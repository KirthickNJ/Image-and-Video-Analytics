# test case 2 : moving vehicle detection
import cv2
import imutils
from matplotlib import pyplot as plt
from IPython.display import clear_output
import time

# Load the video file
cap = cv2.VideoCapture("car.mp4")

# Create background subtractor
fgbg = cv2.createBackgroundSubtractorMOG2(history=500, varThreshold=50)

while cap.isOpened():
    
    ret, frame = cap.read()
    
    if not ret:
        break

    # Resize frame
    frame = imutils.resize(frame, width=700)

    # Apply background subtraction
    fgmask = fgbg.apply(frame)

    # Remove noise
    kernel = cv2.getStructuringElement(cv2.MORPH_RECT,(5,5))
    fgmask = cv2.morphologyEx(fgmask, cv2.MORPH_CLOSE, kernel)

    # Find moving objects
    contours, _ = cv2.findContours(fgmask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    for cnt in contours:
        area = cv2.contourArea(cnt)

        # Ignore small objects
        if area < 2000:
            continue

        x,y,w,h = cv2.boundingRect(cnt)

        # Draw rectangle
        cv2.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),2)
        cv2.putText(frame,"Vehicle",(x,y-10),
                    cv2.FONT_HERSHEY_SIMPLEX,0.6,(0,255,0),2)

    # Convert BGR to RGB for Jupyter display
    frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    clear_output(wait=True)
    plt.imshow(frame_rgb)
    plt.axis("off")
    plt.show()

    time.sleep(0.03)

cap.release()



https://github.com/user-attachments/assets/ecc3490f-1e8d-4a54-8589-cc1f773a2acf

