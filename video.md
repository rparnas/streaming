# Streaming Video Files

## Step 1: OBS and VLC -> VB-Cable and OBS Virtual Webcam
Streaming using a virtual webcam has an advantage in video quality, video and audio stability and required bandwidth (as opposed to streaming using screen share). This setup should only be used with a video card that supports hardware video encoding.

Using this method, any remaining quality bottlenecks seems to be dependent on the streaming server itself (e.g. Discord, Zoom, or one you host yourself). For example, on Discord audio quality is generally poor except at the highest paid 'boost levels'.

When using a virtual webcam to stream, you may wish to stream from one computer while joining the stream as a participant from another computer (especially given the inconvenience of having to change chat application settings when switching from streaming back to everyday usage). Otherwise, see some workarounds below to do everything on the same machine. 

Note that in Discord, Zoom and many other conferencing applications, the video preview of the OBS virtual webcam will be horizontally flipped on the local machine only.

### Step 2: Setup VB-Cable
* A virtual audio input device is required to pass along the audio from the virtual OBS-based webcam. This is because many communication applications can only take audio from devices listed explicitly under *Control Panel \ Sound \ Recording*.
* Download the [VB-CABLE Virtual Audio Device](https://vb-audio.com/Cable/) and run the installer as an administrator.

* Go to both *Control Panel \ Sound \ Playback*. 
  * If a VB-Audio device is not visible, right-click the empty space in the device list and click *Show Disabled Devices* to see the disabled VB-audio device. Right-click the disabled AB-Audio device and choose *Enable*.
  * The VB-Cable installer may have changed the *Default Device* and or the *Default Communication Device* to itself. You may want to revert it back by right-clicking the appropriate device and clicking *Set as the Default Device* and *Set as the Default Communication Device* respectively.
  * Similarly ensure there is an enabled VB-Audio device under *Control Panel \ Sound \ Recording* (and revert any defaults as desired).

### Step 3: Setup Virtual Webcam
* Ensure that [VLC](https://www.videolan.org/vlc/) and [OBS Studio](https://obsproject.com/) are installed. The bittage of both applications must match (i.e. 32 or 64-bit).
* In OBS Studio, right-click the *Sources* list and choose *Add > VLC Video Source*. 
  * Choose the settings from the VLC Video Source as desired, including adding the video files to be streamed to the playlist. The playlist and other settings can be changed at any time by double-clicking on the source in the sources list.
* Under *File > Settings* on the *Audio* tab, ensure that *Advanced \ Monitoring Device* is set to the VB-Audio device.
* Right-click the *Audio Mixers* and choose  *Advanced Audio Properties*. Ensure that under the *Monitoring* column, the VLC audio source is set to *Monitor Only*.
* On the *Audio Mixers* list you may wish to disable other audio sources.
* On the Video Preview, you should right-click the VLC video feed and choose *Resize output (source size)*.
* When you are ready to stream click *Start Virtual Camera* under *Controls* in the main window.

### Step 4: Setup Discord
* In Discord, go to the *User Settings Page* (gear icon)
  * Under *Voice & Video*:
    * Ensure your *Input Device* is set to VB-Audio.
    * Turn off *Automatically determine input sensitivity* and set the sensitivity threshold to the minimum value (-100 dB).
  * Under *Video Settings*:
    * Set *Camera* to the OBS Virtual Camera.
  * Under *Advanced* ensure that the following are disabled:
    * Noise Suppression
    * Echo Cancellation
    * Noise Reduction
    * Advanced Voice Activity (disable if it is not already greyed-out).
    * Automatic Gain Control
    
### Step 4 (Alternative): Setup Zoom
 * **TODO**: Fill-in.
 
### Step 4 (Alternative): Setup Streaming Server (Incomplete)
* Need to look into what [video streaming protocol](https://www.wowza.com/blog/streaming-protocols). Most protocols are not natively implemented by browsers and require a JavaScript video library to decode on the client side.
* Would be nice to continue using OBS Studio for its versatility. It only seems to support RTMP.
* Many seem to be using nginx as the web server, and almost always on Unix.
* The OBS feed as sent to Discord is < 3 Mbps, so 3-4 Mbps per person might be a reasonable estimate of upload bandwidth required.
* The standard Charter Spectrum plan is 100 Mbps download / 10 Mbps upload, but a 200/20 plan looks to be available to most consumers.
* Instead of a "live-streaming" solution could use a similar tech pipeline to deliver known-ahead-of-time video content allowing the web browser to pre-cache. A syncing solution would likely need to be custom-implemented on top.
    
### Appendix A: Additional Notes for Particular Media Files
* The OBS VLC plugin is limited in its ability to control which audio and or subtitles are displayed. You may want to simply create a version of your media file with only the single desired audio and (and single desired subtitle track if applicable).  If using subtitles you may want to set the **Fored Track** flag to **Yes**. Use [MKVToolNix](https://mkvtoolnix.download/) to do this. The executables are Windows are hosted [here](https://www.fosshub.com/MKVToolNix.html).
    
### Appendix B: Workarounds to Host the Stream and Engage in the Stream as a Participant from One Computer 
* To speak on the stream, add your microphone to the OBS Studio audio mixer. Under the *Audio Properties*, under the *Monitor* column, choose *Monitor Only* for this device.
* As a workaround to listen to the audio of the video being streamed run another instance of VLC playing the same video file and sync manually. You can see the timestamp of the VLC video in OBS (as well as the video playback controls) if you click on the VLC source in the OBS preview.
* **TODO:** Come up with something better that supports all types of content. For example, manual sync is not an option for streaming non-video applications.
