---
id: demo_reid_2
title: Basic Reidentification Demo with Two Cameras
hide_title: true
---

# Basic Reidentification Demo with Two Cameras

This section demonstrates the setup and usage of the [Reidentification] feature
in a two-camera system.

The **Basic Reidentifier** microservice processes feature vectors and finds
re-appearances. In the demo, identified people are marked with an orange
bounding box and an auto increment ID. People not identified are marked with
a grey bounding box. It is also possible to calculate the dwell time passed
between the registration and reidentification.

![Basic Reidentification demo](../assets/demo/demo_2-cam_reg.png)  
_Two-Camera System Registration_

![Basic Reidentification demo](../assets/demo/demo_2-cam_reid.png)  
_Two-Camera System Reidentification_

In a two-camera system, registration and reidentification are performed on
separate cameras. A camera has one of the following two roles:

 * **Registration only**:  
   the camera saves people appearing.
 * **Reidentification only**:  
   the camera identifies people previously saved.

## Prerequisites

Before starting the demo, ensure the following:

* UVAP is installed as instructed in [Setting Up UVAP]
* UVAP is configured in `fve` demo mode as instructed in [Configuring UVAP for FVE Demo Mode]
* The following microservices are running:
  * [Multi-Graph Runner]
  * [Basic Reidentifier]
* Web display is started as instructed in [Starting Web Player].

**Basic Reidentifier** microservice requires video(s) with faces larger than 72
pixels, looking straight into the camera.

Required topics:

>**Note:**  
Registration and reidentification are performed on separate cameras.

 * `fve.cam.0.original.Image.jpg`
 * `fve.cam.0.dets.ObjectDetectionRecord.json`
 * `fve.cam.0.fvecs.FeatureVectorRecord.json`
 * `fve.cam.99.reids.ReidRecord.json`
 * `fve.cam.1.original.Image.jpg`
 * `fve.cam.1.dets.ObjectDetectionRecord.json`
 * `fve.cam.1.fvecs.FeatureVectorRecord.json`

## Starting Two-Camera Reidentification Demo

Start the demo with `run_demo.sh`:

   >**Attention!**  
   After the first run of these scripts, execute `set_retention.sh` script
   manually because new (`*.Image.jpg`) topics are created.

     ```
     $ "${UVAP_HOME}"/scripts/run_demo.sh \
       --demo-name basic_reidentification_2 \
       --demo-mode fve -- --net uvap
     ```
   
## Display in Web Browser

Navigate to the following URL to display the demo:
  
   ```
   http://localhost:9999#fve.cam.1.reids.Image.jpg
   ```

[Basic Reidentifier]: ../dev/start_reid.md#starting-basic-reidentifier
[Configuring UVAP for FVE Demo Mode]: demo_config_fve.md#configuring-uvap-for-fve-demo-mode
[Multi-Graph Runner]: ../dev/start_mgr.md#starting-multi-graph-runner
[Reidentification]: ../feat/face_prop/feat_reid.md#reidentification-bsic
[Setting Up UVAP]: ../install/uvap_install_setup.md#setting-up-uvap
[Starting Web Player]: demo_web_player.md#starting-web-player
[Web display]: demo_web_player.md#web-display
