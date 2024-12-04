# PythonProje
from imageai.Detection import ObjectDetection

detector = ObjectDetection()
detector.setModelTypeAsYOLOv3()
detector.setModelPath("yolov3.pt")
detector.loadModel()
detections = detector.detectObjectsFromImage(input_image="C:\Users\erens\Desktop\Mezuniyet P\image\çöp.jpg", output_image_path="imagenew.jpg", minimum_percentage_probability=30)

def detect_objects_on_road(input_image, output_image, model_path):
    detector = ObjectDetection()
    detector.setModelTypeAsYOLOv3()
    detector.setModelPath(model_path)
    detector.loadModel()

    detections = detector.detectObjectsFromImage(
        input_image=input_image,
        output_image_path=output_image,
        minimum_percentage_probability=30
    )

    return detections

def analyze_objects(detections):
    road_objects = []
    if len(detections) > 0:
      for detection in detections:
          if detection["name"] in ["plastic", "glass", "metal", "paper", "organic_waste", 'train', 'electronic']:
              road_objects.append(detection)

    return road_objects

input_image = "C:\Users\erens\Desktop\Mezuniyet P\image\çöp.jpg"
output_image = "output_image.jpg"

detections = detect_objects_on_road(input_image, output_image, "/content/yolov3.pt")
road_objects = analyze_objects(detections)

if len(road_objects) > 0:
  print("Algılanan öğeler:")
  for obj in road_objects:
      print(obj["name"], " : ", obj["percentage_probability"], " : ", obj["box_points"])
else:
   print("Çöp algılanamadı!")
