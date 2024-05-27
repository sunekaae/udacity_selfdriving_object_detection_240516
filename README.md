# udacity_selfdriving_object_detection_240516
object detection course work for udacity's selfdriving car engineer nanodegree 

## Comparison of different configurations
* EfficientDet D1 640x640 (efficientdet_d1_coco17_tpu-32) (default)
  * fine_tune_checkpoint_type: "detection"
  * "Found new checkpoint at /opt/training/ckpt-3"
* SSD MobileNet V2 FPNLite 640x640 (ssd_mobilenet_v2_fpnlite_640x640_coco17_tpu-8)
  * fine_tune_checkpoint_type: "classification"
  * change: fine_tune_checkpoint_type: "classification" -> detection
    * "Found new checkpoint at /opt/training/ckpt-3"
    * resource error in logs. changes to config file needed. Via mentor on help site:
      * change: batch_size: 128 -> 8
      * change: num_steps: 50000 -> 300000
* Faster R-CNN ResNet152 V1 640x640 (faster_rcnn_resnet152_v1_640x640_coco17_tpu-8)
  * fine_tune_checkpoint_type: "classification"
  * Not Working: "No checkpoint specified (save_path=None); nothing is being restored"
  * also does not work with "detection"
* SSD ResNet50 V1 FPN 640x640 (RetinaNet50) (ssd_resnet50_v1_fpn_640x640_coco17_tpu-8)
  * fine_tune_checkpoint_type: "classification"
  * Not working: "Timed-out waiting for a checkpoint." and "No checkpoint specified (save_path=None); nothing is being restored."
  * change to: fine_tune_checkpoint_type: "detection"
    * Found new checkpoint at /opt/training/ckpt-1
    * "ClientError: Please use an instance type with more memory, or reduce the size of job data processed on an instance."
    * adjustment which worked:
      * batch_size: 64 -> 8
      * num_steps: 25000 -> 75000
      * time to execute: 27 minutes.
        * "Found new checkpoint at /opt/training/ckpt-3" and also "Waiting for new checkpoint at /opt/training"
        * seems 2 checkpoints?
* Faster R-CNN ResNet50 V1 640x640 (faster_rcnn_resnet50_v1_640x640_coco17_tpu-8.config)
  * fine_tune_checkpoint_type: "classification"
  * "Timed-out waiting for a checkpoint"
    * trying: change to: fine_tune_checkpoint_type: "detection"
  
   
## chatgpt on classication vs detection
1.	Classification:
	•	Purpose: Used for fine-tuning models that perform image classification tasks.
	•	Model Architecture: The pre-trained model used in this case is typically an image classification model, such as ResNet, VGG, or any other architecture designed to categorize images into predefined classes.
	•	Output: The output of the model is a set of class probabilities for the input image, where each probability corresponds to the likelihood that the image belongs to a particular class.
	•	Training Objective: The objective is to minimize the classification loss (e.g., cross-entropy loss) by adjusting the model weights to correctly classify images into their respective categories.
	•	Example Use Case: Fine-tuning a model to classify images of different breeds of dogs.
	2.	Detection:
	•	Purpose: Used for fine-tuning models that perform object detection tasks.
	•	Model Architecture: The pre-trained model used here is typically an object detection model, such as Faster R-CNN, YOLO, or SSD, which is designed to identify and locate objects within an image.
	•	Output: The output includes both the class probabilities and the bounding box coordinates for each detected object in the image.
	•	Training Objective: The objective is to minimize the detection loss, which usually includes both the classification loss (for the object classes) and the localization loss (for the bounding box coordinates). The model learns to correctly identify and localize objects within an image.
	•	Example Use Case: Fine-tuning a model to detect and localize different types of vehicles in traffic camera footage.

### ie
* Classification: ResNet, VGG
* Detection: Faster R-CNN, YOLO, or SSD,

