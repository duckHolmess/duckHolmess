import cv2
import mediapipe as mp
import numpy as np

# Mediapipe'in pose modelini başlatma
mp_drawing = mp.solutions.drawing_utils
mp_pose = mp.solutions.pose

# Kamerayı başlatma
cap = cv2.VideoCapture(0)

# Pencereyi tam ekran yapma
cv2.namedWindow('Eklemler', cv2.WND_PROP_FULLSCREEN)
cv2.setWindowProperty('Eklemler', cv2.WND_PROP_FULLSCREEN, cv2.WINDOW_FULLSCREEN)

with mp_pose.Pose(min_detection_confidence=0.5, min_tracking_confidence=0.5, model_complexity=1) as pose:
    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            print("Kamera açılamadı.")
            break

        # Görüntüyü BGR'den RGB'ye çevirme ve yatay olarak ters çevirme
        image = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
        image = cv2.flip(image, 1)  # Yatay eksende ters çevirme
        image.flags.writeable = False

       
