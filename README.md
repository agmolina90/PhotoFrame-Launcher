Turn an old Android tablet (Android 6.0 or newer) into a digital photo frame, and send it photos, videos and music from your phone over Wi-Fi. I tested this on my Aluratek - 10" IPS LCD (Model: ACKWS10F) but theorically works on any Android tablet. Claude was used to create the apps. 

This repo has two Android apps:
Folder	App	Install on
PhotoFrame/	Photo Frame: the slideshow app and the receiver	The tablet
PhotoPusher/	Frame Pusher: the companion/remote app	Your phone

Features

Photo Frame (tablet)

Slideshow of photos and videos with many transitions (fade, slide, zoom, flip, spin and more, or random)
Smart layouts: pairs portrait photos side by side and can mix three photos on one screen
Clock and date overlay, with font, size, colour, opacity and corner position settings
Holiday countdown with a picture for each holiday, plus your own special days (birthdays, anniversaries)
Optional photo date and location (from the photo's GPS data) shown on screen
"Paper" looks (matte, glossy, warm, vintage, black and white)
Background music from songs sent from the phone, with separate music and video volumes
Night schedule: dim and/or sleep the screen between set times (tap to wake)
Triple-tap to draw on the screen
Can act as the tablet's home screen (launcher)
Optional USB drive support: show the drive's photos, or copy new ones into the frame's photo folder

Frame Pusher (phone)

Send photos, videos and music to the frame; duplicates are detected and skipped
Videos are converted on the phone to a format Android 6 can play (H.264/AAC MP4, up to 720p)
Choose or create folders on the frame
Remote buttons: Back, Skip, Refresh
Manage (view and delete) photos and music already on the frame
Change all of the frame's settings from the phone
Requirements
Tablet: Android 6.0 (API 23) or newer
Phone: Android 6.0 (API 23) or newer (a recent phone is recommended for video conversion)
Phone and tablet on the same Wi-Fi network

1. Install on the tablet (Photo Frame)
If you are using the Aluratek I referenced use ADB. Install Android platform-tools (it comes with Android Studio, or download it on its own) and make sure adb runs from a terminal. (Right click in the folder where ADB was unzipped, click on the command prompt, type ./adb install photoframe.apk, and press enter.)
If using a different tablet, allow installs from unknown sources (Settings > Security). 
Copy the Photo Frame APK to the tablet (USB cable, cloud drive, etc.) and open it to install, or install over USB with adb install app-debug.apk.
Open Photo Frame and allow the storage permission when asked.

Optional: make it the home screen. Press the tablet's Home button, choose Photo Frame, then Always. To undo it later: Settings > Device > Choose default home app (the exact path varies by tablet).

2. Install on your phone (Frame Pusher)

Install the Frame Pusher APK the same way (allow unknown sources, open the APK). Allow the photo/video permissions when asked. These are also what lets photos keep their location data.

3. Connect the phone to the frame
On the tablet, hold a finger on the screen for 3 seconds to open Settings. Find the Phone app address (an IP address like 192.168.0.118).
In Frame Pusher, tap the gear icon, type that address (numbers only), and tap Save & test connection. You should see "Connected to your frame".
Keep the Photo Frame app open on the tablet while sending.

Tip: give the tablet a fixed IP address in your router so the address doesn't change.

Using it

On the tablet

Hold the screen for 3 seconds: open Settings
Swipe right: next photo. Swipe left: previous photo
Triple-tap: drawing palette (it closes itself after a timeout)

On the phone

Choose photos & videos, then Send to frame
Send to folder picks which folder on the frame receives them
Choose music & send adds songs (turn on "Play music" in Frame settings)
Frame settings changes the frame's look and behaviour remotely
Manage photos on frame and Manage music on frame delete items

Videos: in Frame Pusher's settings (gear icon), "Convert videos for the frame" is on by default. Converting can take about a minute per video. Videos copied from a USB drive are not converted.

USB drive: in the frame's Settings (or Frame settings on the phone), turn on Auto-read USB drive to show a drive's photos without saving them, or Copy USB photos into the photos folder to save new ones to the frame. Copies are named with a content hash, so nothing is saved twice.

Where files are stored on the tablet
Photos and videos: Pictures/PhotoFrame/ (subfolders become folders in the phone app)
Music: Music/PhotoFrame/
How the phone talks to the frame

The frame runs a small HTTP server on port 8080.

Request	Purpose
PUT /upload/<name>[?folder=X]	Save a photo or video (?kind=music for a song)
GET /has/<hash>	Is this file already on the frame?
GET /list, /folders, /musiclist	List photos, folders, songs
GET /thumb/<name>	Thumbnail
DELETE /file/<name>, DELETE /music/<name>	Delete
/move/<name>?to=<folder>	Move to a folder
GET / PUT /prefs	Read or change settings
GET / PUT /events	Read or change special days
/next, /prev, /refresh	Remote control
Security note

The frame's server has no password or encryption. Anyone on the same Wi-Fi network can upload, delete or change settings. Use it on a network you trust, and don't expose port 8080 to the internet.

Troubleshooting
Phone says it can't reach the frame: check both devices are on the same Wi-Fi, the Photo Frame app is open, and the address is correct. Some guest networks block device-to-device traffic.
A video won't play on the tablet: re-send it from Frame Pusher with video conversion on, then delete the old copy in Manage photos on frame.
No photos appear: make sure the storage permission was granted on the tablet, then use Refresh.
Build fails: make sure you opened PhotoFrame or PhotoPusher directly (not the repo root) and that Gradle could download dependencies.
Project layout
PhotoFrame/    Tablet app (slideshow, settings, HTTP receiver)
PhotoPusher/   Phone app (sender, remote, frame settings, video converter)

Co-Authored-By: Claude <noreply@anthropic.com>
