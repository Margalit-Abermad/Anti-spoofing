## Python Anti-spoofing project
### Listens to the streaming of the camera and returns whether the face in front of the camera is real or from a phone / paper / video...

#### בתחילה מתקינים את הספריות של הזיהוי פנים וכו', ואח"כ את אלו:
1. cvzon
2. ultralytics
3. mediapip
#### בהתחלה לא התקין לי את ultralytics אז פתיתי את הניתוב של ה- pip של הפרויקט הזה ועשיתי
>python -m pip install --upgrade pip

#### ואחר כך-

C:\Users\user\Desktop\All Python\בשימוש יומי\פייתון שאני כתבתי\AntiSpoofing\venv\Scripts>pip install ultralytics Collecting ultralytics

#### ואז בסטינגס של הפרויקט ועבד מעולה.

### שלב 1-
#### התחלתי עם לכתוב קבצים לתיקיית Test Scripts
## קובץ faceDetectorFace-
#### לקובץ הזה עשיתי import ל- from cvzone.FaceDetectionModule import FaceDetector
#### ואז ב- ctrl + לחיצה על FaceDetector נפתח לי קוד המקור.
#### ממנו העתקתי את הקוד:



    cap = cv2.VideoCapture(0)
    
    # Initialize the FaceDetector object
    # minDetectionCon: Minimum detection confidence threshold
    # modelSelection: 0 for short-range detection (2 meters), 1 for long-range detection (5 meters)
    detector = FaceDetector(minDetectionCon=0.5, modelSelection=0)
    
    # Run the loop to continually get frames from the webcam
    while True:
        # Read the current frame from the webcam
        # success: Boolean, whether the frame was successfully grabbed
        # img: the captured frame
        success, img = cap.read()
    
        # Detect faces in the image
        # img: Updated image
        # bboxs: List of bounding boxes around detected faces
        img, bboxs = detector.findFaces(img, draw=False)
    
        # Check if any face is detected
        if bboxs:
            # Loop through each bounding box
            for bbox in bboxs:
                # bbox contains 'id', 'bbox', 'score', 'center'
    
                # ---- Get Data  ---- #
                center = bbox["center"]
                x, y, w, h = bbox['bbox']
                score = int(bbox['score'][0] * 100)
    
                # ---- Draw Data  ---- #
                cv2.circle(img, center, 5, (255, 0, 255), cv2.FILLED)
                cvzone.putTextRect(img, f'{score}%', (x, y - 10))
                cvzone.cornerRect(img, (x, y, w, h))
    
        # Display the image in a window named 'Image'
        cv2.imshow("Image", img)
        # Wait for 1 millisecond, and keep the window open
        cv2.waitKey(1)


#### שיניתי את המצלמה ל- 0... (במקור היה על 2.
