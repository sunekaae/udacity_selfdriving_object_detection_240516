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
      * change: num_steps: 300000 -> 50000
* Faster R-CNN ResNet152 V1 640x640 (faster_rcnn_resnet152_v1_640x640_coco17_tpu-8)
  * fine_tune_checkpoint_type: "classification"
  * Not Working: "No checkpoint specified (save_path=None); nothing is being restored"
  * also does not work with "detection"
* SSD ResNet50 V1 FPN 640x640 (RetinaNet50) (ssd_resnet50_v1_fpn_640x640_coco17_tpu-8)
  * fine_tune_checkpoint_type: "classification"
  * Not working: "Timed-out waiting for a checkpoint." and "No checkpoint specified (save_path=None); nothing is being restored."
  * change to: fine_tune_checkpoint_type: "detection"
    * Found new checkpoint at /opt/training/ckpt-1

