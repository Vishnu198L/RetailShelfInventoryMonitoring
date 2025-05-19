from ultralytics import YOLO
import cv2

# Load YOLOv8 model
model = YOLO('yolov8n.pt')  # Swap with your trained model if needed

# Load image
image_path = 'shelf_or_wall.jpg'  # Replace with your actual image path
image = cv2.imread(image_path)

# Run detection
results = model(image)[0]

# Count detected objects (no class check)
object_count = len(results.boxes)

# Draw bounding boxes (optional for visual feedback)
for box in results.boxes:
    x1, y1, x2, y2 = map(int, box.xyxy[0])
    cv2.rectangle(image, (x1, y1), (x2, y2), (0, 255, 0), 2)

# Add object count on image
cv2.putText(image, f'Objects: {object_count}', (30, 40),
            cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 0, 0), 2)

# Show result
cv2.imshow("Wall Detection Count", image)
cv2.waitKey(0)
cv2.destroyAllWindows()

# Print to console too
print(f"Total objects detected: {object_count}")
