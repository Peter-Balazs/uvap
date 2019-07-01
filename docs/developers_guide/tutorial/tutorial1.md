# Tutorial 1 - Start, stop MGR and dump detections

In this tutorial we will star/stop mgr with a simple dataflow graph and dump detection results from kafka.

## Prerequisites


## Steps

### Step 1 - Start MGR with a simple graph


```
# loads the necessary engines
engines_file: "/opt/ultinous/models/engines/head_det.prototxt"

environment:
{
  debug_level: 4
  profile: true
  analysis_thread_count: 2
  gui: NORMAL
  drop_off: {}
  kafka_broker_list: "localhost:9092"
}

data_run:
{
  input:
  {
    file_name: "/dev/video0"  # input is device 0, typically the webcam
  }

  data_flow:
  {
    data_node: {type: FRAME name: "input"}      # always have to have the input frame
    data_node: {type: DETECTIONS name: "detections"}

    process_node:
    {
      type: OBJ_DETECTOR
      name: "head_detector"
      logging: false
      obj_det_config:
      {
        type: HEAD
        input: "input"              # connects to the input data node
        bounding_boxes: "detections"
        min_height_in_pixels: 16
        max_height_in_pixels: 256
        confidence_threshold: 0.95  # look for high confidence detections
        image_scale_factor: 0.5     # downscale image by a factor of 2
      }
    }

    # write detections to a kafka stream
    process_node:
    {
      type: KAFKA_OUTPUT
      name: "kafka_output_detections"
      kafka_output_config:
      {
        topic_name: "demo.cam.0.dets.ObjectDetectionRecord.json"
        input_node: "detections"    # connect to the detections data node
      }
    }
  }
}
```
