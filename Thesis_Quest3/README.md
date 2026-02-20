# Unity-PassthroughCameraApiSamples (Custom Fork)

## Customizations in This Fork
- Stable 2D/3D overlays for YOLO detections with billboarding, pooling, and fallback sprites/meshes. See [Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/SentisInferenceUiManager.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/SentisInferenceUiManager.cs).
- Tool pose stabilization: temporal matching, RMS rejection, low-pass, optional per-axis Kalman filter, screen-space clamp, local offsets, and attachable prefab that follows the pose. See [Assets/PassthroughCameraApiSamples/MultiObjectDetection/ToolPose/Scripts/ToolPoseEstimator.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/ToolPose/Scripts/ToolPoseEstimator.cs).
- Performance logging: periodic console logs for FPS, latency (end-to-end vs. inference-only), pose RMS, position/depth/distance, and per-frame movement deltas. See [Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/PerformanceLogger.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/PerformanceLogger.cs) and [Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/SentisInferenceRunManager.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/SentisInferenceRunManager.cs).
- External YOLO over UDP (PC): Unity listener for normalized detection JSON to drive in-headset overlays. See [Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/YoloListener.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/SentisInference/Scripts/YoloListener.cs); pair with the provided Python sender (captures a PC window, runs YOLO, streams detections over UDP).
- Attached 3D markers: configurable prefab attached to the stabilized tool pose, enabled/disabled with solve validity. See [Assets/PassthroughCameraApiSamples/MultiObjectDetection/ToolPose/Scripts/ToolPoseEstimator.cs](Assets/PassthroughCameraApiSamples/MultiObjectDetection/ToolPose/Scripts/ToolPoseEstimator.cs).

## Quick Usage Notes
- Assign `PerformanceLogger` in your scene, set `poseTarget` to the tool pose transform (or leave blank to fallback to `ToolPoseEstimator.WorldFromTool`).
- In `SentisInferenceRunManager`, `LastInferenceMs` measures model execution; `LastEndToEndMs` measures capture-to-draw.
- In `SentisInferenceUiManager`, set `m_maxDetections` to cap per-frame boxes and choose between 2D sprites or 3D markers.
- For external YOLO: run the Python sender on PC, set Quest IP/port, and add `YoloListener` to a world-space canvas.
