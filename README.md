Open each folder (PhotoFrame, PhotoPusher) separately in Android Studio (Gradle 8.5 is pinned), then Build > Build APK.
PhotoFrame -> install on the tablet. PhotoPusher -> install on your phone.
Frame: hold a finger on the screen for 3 seconds to open Settings.
Launcher: press the Home button and choose Photo Frame > Always. Undo via Settings > Device > Choose default home app.

Changes in this version
- Phone app converts videos to H.264/AAC MP4 (max 720p) before sending, so Android 6 tablets can play them.
  Toggle: Frame Pusher > gear > "Convert videos for the frame". Re-send old videos to get a playable copy,
  then delete the old unplayable ones in "Manage photos on frame".
- Remote buttons (Back / Skip / Refresh): aligned, show a status line, and the frame now always obeys them.
- New setting "Copy USB photos into the photos folder" (frame Settings and phone Frame settings): plugging in a USB drive saves new photos/videos to the frame automatically, skipping ones already saved. USB videos are copied as-is (not converted).
- Holiday picture beside the countdown is now a real ImageView.
Note: both apps now need Gradle to download media3 libraries (internet on first build).
