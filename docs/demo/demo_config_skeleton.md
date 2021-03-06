# Configuring UVAP for Skeleton Demo Mode

To configure UVAP for `skeleton` demo mode:

```
$ "${UVAP_HOME}"/scripts/config.sh --stream-uri [STREAM_URI] \
  --demo-mode skeleton
```

Replace `[STREAM_URI]` with a valid video file or stream:  
  
  * An IP camera, for example:
  
    ```
    rtsp://192.168.0.1/
    ```
  
    The Stream URI can also contain username and password if the stream is
    protected, for example:
  
    ```
    rtsp://username:password@192.168.0.1/
    ```

  * A USB device, for example:
  
    ```
    /dev/video0
    ```

  * A pre-recorded video
  
  Multiple streams to be analyzed may be configured by using more
  `--stream-uri [STREAM_URI]` parameter pairs, for example:

  ```
  $ "${UVAP_HOME}"/scripts/config.sh \
    --stream-uri "rtsp://192.168.0.1/" \
    --stream-uri "rtsp://username:password@192.168.0.2/" \
    --stream-uri "rtsp://192.168.0.3/" \
    --demo-mode skeleton
  ```
 
  The Stream URI(s) can be changed later by running this configuration
  script again.

There are more optional parameters for the `config.sh` script to
override defaults. Use the `--help` parameter to get more details. 
