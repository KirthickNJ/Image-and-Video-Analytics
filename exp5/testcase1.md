# test case 1 : human walking detection
import cv2
import imutils
from matplotlib import pyplot as plt
from IPython.display import clear_output
import time

# Initialize HOG person detector
hog = cv2.HOGDescriptor()
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())





# Load video
cap = cv2.VideoCapture("human.mp4")

while cap.isOpened():
    ret, frame = cap.read()
    
    if not ret:
        break

    # Resize frame
    frame = imutils.resize(frame, width=600)

    # Detect humans
    boxes, weights = hog.detectMultiScale(
        frame,
        winStride=(8,8),
        padding=(16,16),
        scale=1.05
    )

    # Draw boxes
    for (x, y, w, h) in boxes:
        cv2.rectangle(frame, (x,y), (x+w, y+h), (0,255,0), 2)
        cv2.putText(frame, "Person", (x, y-10),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.6, (0,255,0), 2)

    # Convert BGR → RGB for display
    frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    clear_output(wait=True)
    plt.imshow(frame_rgb)
    plt.axis("off")
    plt.show()

    time.sleep(0.03)

cap.release()


https://github.com/user-attachments/assets/41cb83ee-7cae-4980-aa35-211c05b7af13
