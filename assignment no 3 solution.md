|||
| :- | :- |



**Assignment NO 3**

**Topic: Media Recorder Class (Audio & Video Recorder Apps)**














**Name:** Rizwan Khalid.
**Roll No:** 36.
**Class:** BSSE E2.
**Subject:** Application Development 
**Submitted to: S**ir Yousaf.**


**Audio Recorder in Android with Example**

Last Updated : 24, Apr, 2022

In Android for recording audio or video, there is a built-in class called **MediaRecorder**. This class in Android helps to easily record video and audio files. The Android multimedia framework provides built-in support for capturing and encoding common audio and video formats. In android for recording audio, we will use a device microphone along with **MediaRecorder** Class and for recording video, we will use the user’s device Camera and **MediaRecorder** Class. Now in this article, we will see the implementation of an audio recorder in Android with an example. 

**Important Methods of MediaRecorder Class**

|**Method** |**Description**|
| :- | :- |
|setAudioSource()|This method will specify the source of the audio to be recorded.|
|setAudioEncoder()|This method is used to specify the audio encoder.|
|setOutputFormat()|This method is used to specify the output format of our audio.|
|setOutputFile()|This method is used to specify the path of recorded audio files that are to be stored.|
|stop()|This method is used to stop the recording process. |
|start()|This method is used to start the recording process. |
|release()|This method is used to release the resource that is associated with the Media recorder class.|

**Example**

Now we are creating a simple audio recorder app in which we will record audio from users device microphone and then we will store this audio recording in users device. We will also play this saved audio recording. A sample GIF is given below to get an idea about what we are going to do in this article. Note that we are going to implement this project using the **Java** language. 

**Step by Step Implementation**

**Step 1: Create a New Project**

To create a new project in Android Studio please refer to [How to Create/Start a New Project in Android Studio](https://www.geeksforgeeks.org/android-how-to-create-start-a-new-project-in-android-studio/). Note that select **Java** as the programming language. 

**Step 2: Add permissions in the AndroidManifest.xml file**

Add below line in the **AndroidManifest.xml** file. 

- XML

|<p><?**xml** version="1.0" encoding="utf-8"?></p><p><**manifest** xmlns:android="<http://schemas.android.com/apk/res/android>"</p><p>`    `xmlns:tools="<http://schemas.android.com/tools>"</p><p>`    `package="com.gtappdevelopers.camviewlibrary"></p><p> </p><p>`    `<!--Permission for recording audio and storage of audio in users device--></p><p>`    `<**uses-permission** android:name="android.permission.RECORD\_AUDIO"/></p><p>`    `<**uses-permission** android:name="android.permission.WRITE\_EXTERNAL\_STORAGE"/></p><p>`    `<**uses-permission** android:name="android.permission.STORAGE"/></p><p> </p><p> </p><p>`    `<**application**</p><p>`        `android:allowBackup="true"</p><p>`        `android:icon="@mipmap/ic\_launcher"</p><p>`        `android:label="@string/app\_name"</p><p>`        `android:roundIcon="@mipmap/ic\_launcher\_round"</p><p>`        `android:supportsRtl="true"</p><p>`        `android:theme="@style/Theme.CamViewLibrary"></p><p>`        `<**activity** android:name=".MainActivity"></p><p>`            `<**intent-filter**></p><p>`                `<**action** android:name="android.intent.action.MAIN" /></p><p> </p><p>`                `<**category** android:name="android.intent.category.LAUNCHER" /></p><p>`            `</**intent-filter**></p><p>`        `</**activity**></p><p>`    `</**application**></p><p> </p><p></**manifest**></p>|
| :- |

**Step 3: Modify the colors.xml and strings.xml file**

Below is the code for the **colors.xml** file. 

- XML

|<p><?**xml** version="1.0" encoding="utf-8"?></p><p><**resources**></p><p>`    `<**color** name="purple\_200">#0F9D58</**color**></p><p>`    `<**color** name="purple\_500">#0F9D58</**color**></p><p>`    `<**color** name="purple\_700">#0F9D58</**color**></p><p>`    `<**color** name="teal\_200">#FF03DAC5</**color**></p><p>`    `<**color** name="teal\_700">#FF018786</**color**></p><p>`    `<**color** name="black">#FF000000</**color**></p><p>`    `<**color** name="white">#FFFFFFFF</**color**></p><p>`    `<**color** name="gray">#A39696</**color**></p><p></**resources**></p>|
| :- |

Below is the code for the **strings.xml** file. 

- XML

|<p><**resources**></p><p>`    `<**string** name="app\_name">GFG APP</**string**></p><p>`    `<**string** name="toggle\_flash">Toggle Flash</**string**></p><p>`    `<**string** name="action\_settings">Settings</**string**></p><p>`    `<**string** name="scanned\_data">Scanned Data</**string**></p><p>`    `<**string** name="audio\_recorder">Audio Recorder</**string**></p><p>`    `<**string** name="start\_recording">Start Recording</**string**></p><p>`    `<**string** name="stop\_recording">Stop Recording</**string**></p><p>`    `<**string** name="play\_recording">Play Recording</**string**></p><p>`    `<**string** name="stop\_playing">Stop Playing</**string**></p><p>`    `<**string** name="status">Status</**string**></p><p></**resources**></p>|
| :- |

**Step 4: Working with the activity\_main.xml file**

Navigate to the **app > res > layout > activity\_main.xml**. Below is the code for the **activity\_main.xml** file. Comments are added inside the code to understand the code in more detail. 

- XML

|<p><?**xml** version="1.0" encoding="utf-8"?></p><p><!--XML code for activity\_main.xml--></p><p><**RelativeLayout**</p><p>`    `xmlns:android="<http://schemas.android.com/apk/res/android>"</p><p>`    `xmlns:app="<http://schemas.android.com/apk/res-auto>"</p><p>`    `xmlns:tools="<http://schemas.android.com/tools>"</p><p>`    `android:layout\_width="match\_parent"</p><p>`    `android:layout\_height="match\_parent"</p><p>`    `android:orientation="horizontal"</p><p>`    `tools:context=".MainActivity"></p><p> </p><p>`    `<!--Heading Text View--></p><p>`    `<**TextView**</p><p>`        `android:id="@+id/txthead"</p><p>`        `android:layout\_width="match\_parent"</p><p>`        `android:layout\_height="wrap\_content"</p><p>`        `android:layout\_centerHorizontal="true"</p><p>`        `android:text="@string/audio\_recorder"</p><p>`        `android:textAlignment="center"</p><p>`        `android:textColor="@color/black"</p><p>`        `android:textSize="30sp" /></p><p> </p><p>`    `<!--This will display the status of our app when </p><p>`        `we will record some audio and play that audio--></p><p>`    `<**TextView**</p><p>`        `android:id="@+id/idTVstatus"</p><p>`        `android:layout\_width="match\_parent"</p><p>`        `android:layout\_height="wrap\_content"</p><p>`        `android:layout\_marginTop="150dp"</p><p>`        `android:text="@string/status"</p><p>`        `android:textAlignment="center"</p><p>`        `android:textSize="18sp" /></p><p> </p><p>`    `<!--Linear Layout for adding textviews</p><p>`        `in horizontal manner--></p><p>`    `<**LinearLayout**</p><p>`        `android:layout\_width="match\_parent"</p><p>`        `android:layout\_height="wrap\_content"</p><p>`        `android:layout\_centerInParent="true"</p><p>`        `android:layout\_marginTop="30dp"</p><p>`        `android:orientation="horizontal"</p><p>`        `android:weightSum="4"></p><p> </p><p>`        `<!--Textview to start audio recording</p><p>`            `drawableTop will add above mic image--></p><p>`        `<**TextView**</p><p>`            `android:id="@+id/btnRecord"</p><p>`            `android:layout\_width="0dp"</p><p>`            `android:layout\_height="wrap\_content"</p><p>`            `android:layout\_margin="5dp"</p><p>`            `android:layout\_weight="1"</p><p>`            `android:background="@color/purple\_500"</p><p>`            `android:padding="5dp"</p><p>`            `android:text="@string/start\_recording"</p><p>`            `android:textAlignment="center"</p><p>`            `android:textColor="@color/white"</p><p>`            `app:drawableTopCompat="@drawable/ic\_start\_recording" /></p><p> </p><p>`        `<!--Textview to stop audio recording</p><p>`            `drawableTop will add above mic image--></p><p>`        `<**TextView**</p><p>`            `android:id="@+id/btnStop"</p><p>`            `android:layout\_width="0dp"</p><p>`            `android:layout\_height="wrap\_content"</p><p>`            `android:layout\_margin="5dp"</p><p>`            `android:layout\_weight="1"</p><p>`            `android:background="@color/purple\_500"</p><p>`            `android:padding="5dp"</p><p>`            `android:text="@string/stop\_recording"</p><p>`            `android:textAlignment="center"</p><p>`            `android:textColor="@color/white"</p><p>`            `app:drawableTopCompat="@drawable/ic\_stop\_recording" /></p><p> </p><p>`        `<!--Textview to play audio that is recorded</p><p>`            `drawableTop will add above mic image--></p><p>`        `<**TextView**</p><p>`            `android:id="@+id/btnPlay"</p><p>`            `android:layout\_width="0dp"</p><p>`            `android:layout\_height="wrap\_content"</p><p>`            `android:layout\_margin="5dp"</p><p>`            `android:layout\_weight="1"</p><p>`            `android:background="@color/purple\_500"</p><p>`            `android:padding="5dp"</p><p>`            `android:text="@string/play\_recording"</p><p>`            `android:textAlignment="center"</p><p>`            `android:textColor="@color/white"</p><p>`            `app:drawableTopCompat="@drawable/ic\_play\_audio" /></p><p> </p><p>`        `<!--Textview to pause the play of audio recording</p><p>`            `drawableTop will add above mic image--></p><p>`        `<**TextView**</p><p>`            `android:id="@+id/btnStopPlay"</p><p>`            `android:layout\_width="0dp"</p><p>`            `android:layout\_height="wrap\_content"</p><p>`            `android:layout\_margin="5dp"</p><p>`            `android:layout\_weight="1"</p><p>`            `android:background="@color/purple\_500"</p><p>`            `android:lines="2"</p><p>`            `android:padding="5dp"</p><p>`            `android:text="@string/stop\_playing"</p><p>`            `android:textAlignment="center"</p><p>`            `android:textColor="@color/white"</p><p>`            `app:drawableTopCompat="@drawable/ic\_pause\_audio" /></p><p> </p><p>`    `</**LinearLayout**></p><p></**RelativeLayout**></p>|
| :- |

**Step 5: Working with the MainActivity.java file**

Navigate to the **app > java > Your app’s package name > MainActivity.java**. Below is the code for the **MainActivity.java** file. Comments are added inside the code to understand the code in more detail. 

- Java

|<p>**import** android.content.pm.PackageManager;</p><p>**import** android.media.MediaPlayer;</p><p>**import** android.media.MediaRecorder;</p><p>**import** android.os.Bundle;</p><p>**import** android.os.Environment;</p><p>**import** android.util.Log;</p><p>**import** android.view.View;</p><p>**import** android.widget.TextView;</p><p>**import** android.widget.Toast;</p><p> </p><p>**import** androidx.appcompat.app.AppCompatActivity;</p><p>**import** androidx.core.app.ActivityCompat;</p><p>**import** androidx.core.content.ContextCompat;</p><p> </p><p>**import** java.io.IOException;</p><p> </p><p>**import** **static** android.Manifest.permission.RECORD\_AUDIO;</p><p>**import** **static** android.Manifest.permission.WRITE\_EXTERNAL\_STORAGE;</p><p> </p><p>**public** **class** MainActivity **extends** AppCompatActivity {</p><p> </p><p>`    `// Initializing all variables..</p><p>`    `**private** TextView startTV, stopTV, playTV, stopplayTV, statusTV;</p><p>     </p><p>`    `// creating a variable for media recorder object class.</p><p>`    `**private** MediaRecorder mRecorder;</p><p>     </p><p>`    `// creating a variable for mediaplayer class</p><p>`    `**private** MediaPlayer mPlayer;</p><p>     </p><p>`    `// string variable is created for storing a file name</p><p>`    `**private** **static** String mFileName = **null**;</p><p>     </p><p>`    `// constant for storing audio permission</p><p>`    `**public** **static** **final** **int** REQUEST\_AUDIO\_PERMISSION\_CODE = 1;</p><p> </p><p>`    `@Override</p><p>`    `**protected** **void** onCreate(Bundle savedInstanceState) {</p><p>`        `**super**.onCreate(savedInstanceState);</p><p>`        `setContentView(R.layout.activity\_main);</p><p>         </p><p>`        `// initialize all variables with their layout items.</p><p>`        `statusTV = findViewById(R.id.idTVstatus);</p><p>`        `startTV = findViewById(R.id.btnRecord);</p><p>`        `stopTV = findViewById(R.id.btnStop);</p><p>`        `playTV = findViewById(R.id.btnPlay);</p><p>`        `stopplayTV = findViewById(R.id.btnStopPlay);</p><p>`        `stopTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `playTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p> </p><p>`        `startTV.setOnClickListener(**new** View.OnClickListener() {</p><p>`            `@Override</p><p>`            `**public** **void** onClick(View v) {</p><p>`                `// start recording method will </p><p>`                `// start the recording of audio.</p><p>`                `startRecording();</p><p>`            `}</p><p>`        `});</p><p>`        `stopTV.setOnClickListener(**new** View.OnClickListener() {</p><p>`            `@Override</p><p>`            `**public** **void** onClick(View v) {</p><p>`                `// pause Recording method will </p><p>`                `// pause the recording of audio.</p><p>`                `pauseRecording();</p><p> </p><p>`            `}</p><p>`        `});</p><p>`        `playTV.setOnClickListener(**new** View.OnClickListener() {</p><p>`            `@Override</p><p>`            `**public** **void** onClick(View v) {</p><p>`                `// play audio method will play </p><p>`                `// the audio which we have recorded</p><p>`                `playAudio();</p><p>`            `}</p><p>`        `});</p><p>`        `stopplayTV.setOnClickListener(**new** View.OnClickListener() {</p><p>`            `@Override</p><p>`            `**public** **void** onClick(View v) {</p><p>`                `// pause play method will </p><p>`                `// pause the play of audio</p><p>`                `pausePlaying();</p><p>`            `}</p><p>`        `});</p><p>`    `}</p><p> </p><p>`    `**private** **void** startRecording() {</p><p>`        `// check permission method is used to check</p><p>`        `// that the user has granted permission </p><p>`        `// to record and store the audio.</p><p>`        `**if** (CheckPermissions()) {</p><p>             </p><p>`            `// setbackgroundcolor method will change</p><p>`            `// the background color of text view.</p><p>`            `stopTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`            `startTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`            `playTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`            `stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>            </p><p>`            `// we are here initializing our filename variable</p><p>`            `// with the path of the recorded audio file.</p><p>`            `mFileName = Environment.getExternalStorageDirectory().getAbsolutePath();</p><p>`            `mFileName += "/AudioRecording.3gp";</p><p>             </p><p>`            `// below method is used to initialize </p><p>`            `// the media recorder class</p><p>`            `mRecorder = **new** MediaRecorder();</p><p>             </p><p>`            `// below method is used to set the audio </p><p>`            `// source which we are using a mic.</p><p>`            `mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);</p><p>             </p><p>`            `// below method is used to set </p><p>`            `// the output format of the audio.</p><p>`            `mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE\_GPP);</p><p>             </p><p>`            `// below method is used to set the </p><p>`            `// audio encoder for our recorded audio.</p><p>`            `mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR\_NB);</p><p>             </p><p>`            `// below method is used to set the </p><p>`            `// output file location for our recorded audio</p><p>`            `mRecorder.setOutputFile(mFileName);</p><p>`            `**try** {</p><p>`                `// below method will prepare</p><p>`                `// our audio recorder class</p><p>`                `mRecorder.prepare();</p><p>`            `} **catch** (IOException e) {</p><p>`                `Log.e("TAG", "prepare() failed");</p><p>`            `}</p><p>`            `// start method will start </p><p>`            `// the audio recording.</p><p>`            `mRecorder.start();</p><p>`            `statusTV.setText("Recording Started");</p><p>`        `} **else** {</p><p>`            `// if audio recording permissions are</p><p>`            `// not granted by user below method will</p><p>`            `// ask for runtime permission for mic and storage.</p><p>`            `RequestPermissions();</p><p>`        `}</p><p>`    `}</p><p> </p><p>`    `@Override</p><p>`    `**public** **void** onRequestPermissionsResult(**int** requestCode, String[] permissions, **int**[] grantResults) {</p><p>`        `// this method is called when user will</p><p>`        `// grant the permission for audio recording.</p><p>`        `**switch** (requestCode) {</p><p>`            `**case** REQUEST\_AUDIO\_PERMISSION\_CODE:</p><p>`                `**if** (grantResults.length > 0) {</p><p>`                    `**boolean** permissionToRecord = grantResults[0] == PackageManager.PERMISSION\_GRANTED;</p><p>`                    `**boolean** permissionToStore = grantResults[1] == PackageManager.PERMISSION\_GRANTED;</p><p>`                    `**if** (permissionToRecord && permissionToStore) {</p><p>`                        `Toast.makeText(getApplicationContext(), "Permission Granted", Toast.LENGTH\_LONG).show();</p><p>`                    `} **else** {</p><p>`                        `Toast.makeText(getApplicationContext(), "Permission Denied", Toast.LENGTH\_LONG).show();</p><p>`                    `}</p><p>`                `}</p><p>`                `**break**;</p><p>`        `}</p><p>`    `}</p><p> </p><p>`    `**public** **boolean** CheckPermissions() {</p><p>`        `// this method is used to check permission</p><p>`        `**int** result = ContextCompat.checkSelfPermission(getApplicationContext(), WRITE\_EXTERNAL\_STORAGE);</p><p>`        `**int** result1 = ContextCompat.checkSelfPermission(getApplicationContext(), RECORD\_AUDIO);</p><p>`        `**return** result == PackageManager.PERMISSION\_GRANTED && result1 == PackageManager.PERMISSION\_GRANTED;</p><p>`    `}</p><p> </p><p>`    `**private** **void** RequestPermissions() {</p><p>`        `// this method is used to request the</p><p>`        `// permission for audio recording and storage.</p><p>`        `ActivityCompat.requestPermissions(MainActivity.**this**, **new** String[]{RECORD\_AUDIO, WRITE\_EXTERNAL\_STORAGE}, REQUEST\_AUDIO\_PERMISSION\_CODE);</p><p>`    `}</p><p> </p><p> </p><p>`    `**public** **void** playAudio() {</p><p>`        `stopTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `startTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`        `playTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `stopplayTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>         </p><p>`        `// for playing our recorded audio</p><p>`        `// we are using media player class.</p><p>`        `mPlayer = **new** MediaPlayer();</p><p>`        `**try** {</p><p>`            `// below method is used to set the</p><p>`            `// data source which will be our file name</p><p>`            `mPlayer.setDataSource(mFileName);</p><p>             </p><p>`            `// below method will prepare our media player</p><p>`            `mPlayer.prepare();</p><p>             </p><p>`            `// below method will start our media player.</p><p>`            `mPlayer.start();</p><p>`            `statusTV.setText("Recording Started Playing");</p><p>`        `} **catch** (IOException e) {</p><p>`            `Log.e("TAG", "prepare() failed");</p><p>`        `}</p><p>`    `}</p><p> </p><p>`    `**public** **void** pauseRecording() {</p><p>`        `stopTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `startTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`        `playTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`        `stopplayTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>         </p><p>`        `// below method will stop </p><p>`        `// the audio recording.</p><p>`        `mRecorder.stop();</p><p>         </p><p>`        `// below method will release </p><p>`        `// the media recorder class.</p><p>`        `mRecorder.release();</p><p>`        `mRecorder = **null**;</p><p>`        `statusTV.setText("Recording Stopped");</p><p>`    `}</p><p> </p><p>`    `**public** **void** pausePlaying() {</p><p>`        `// this method will release the media player</p><p>`        `// class and pause the playing of our recorded audio.</p><p>`        `mPlayer.release();</p><p>`        `mPlayer = **null**;</p><p>`        `stopTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `startTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`        `playTV.setBackgroundColor(getResources().getColor(R.color.purple\_200));</p><p>`        `stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));</p><p>`        `statusTV.setText("Recording Play Stopped");</p><p>`    `}</p><p>}</p>|
| :- |

All drawables are stored in the drawable folder. Navigate to the app > res > drawable folder to see all drawables. Now run the app on the Physical device to test it.  











# **MediaRecorder overview**
` `bookmark\_border

The Android multimedia framework includes support for capturing and encoding a variety of common audio and video formats. You can use the [MediaRecorder](https://developer.android.com/reference/android/media/MediaRecorder) APIs if supported by the device hardware.

This document shows you how to use MediaRecorder to write an application that captures audio from a device microphone, save the audio, and play it back (with [MediaPlayer](https://developer.android.com/reference/android/media/MediaPlayer)). To record video you'll need to use the device's camera along with MediaRecorder. This is described in the [Camera](https://developer.android.com/guide/topics/media/camera) guide.

**Note:** The Android Emulator cannot record audio. Be sure to test your code on a real device that can record.

**Requesting permission to record audio**

To be able to record, your app must tell the user that it will access the device's audio input. You must include this permission tag in the app's manifest file:

<uses-permission android:name="android.permission.RECORD\_AUDIO" />

RECORD\_AUDIO is considered a ["dangerous" permission](https://developer.android.com/guide/topics/permissions/requesting#normal-dangerous) because it may pose a risk to the user's privacy. Starting with Android 6.0 (API level 23) an app that uses a dangerous permission must ask the user for approval at run time. After the user has granted permission, the app should remember and not ask again. The sample code below shows how to implement this behavior using [ActivityCompat.requestPermissions()](https://developer.android.com/reference/androidx/core/app/ActivityCompat#requestPermissions\(android.app.Activity,%20java.lang.String[],%20int\)).

**Creating and running a MediaRecorder**

Initialize a new instance of [MediaRecorder](https://developer.android.com/reference/android/media/MediaRecorder) with the following calls:

- Set the audio source using [setAudioSource()](https://developer.android.com/reference/android/media/MediaRecorder#setAudioSource\(int\)). You'll probably use [MIC](https://developer.android.com/reference/android/media/MediaRecorder.AudioSource#MIC).

  **Note:** Most of the audio sources (including **DEFAULT**) apply processing to the audio signal. To record raw audio select [**UNPROCESSED**](https://developer.android.com/reference/android/media/MediaRecorder.AudioSource#UNPROCESSED). Some devices do not support unprocessed input. Call [**AudioManager.getProperty(AudioManager.PROPERTY_SUPPORT_AUDIO_SOURCE_UNPROCESSED)**](https://developer.android.com/reference/android/media/AudioManager#getProperty\(java.lang.String\)) first to verify it's available. If it is not, try using [**VOICE_RECOGNITION**](https://developer.android.com/reference/android/media/MediaRecorder.AudioSource#VOICE_RECOGNITION) instead, which does not employ AGC or noise suppression. You can use **UNPROCESSED** as an audio source even when the property is not supported, but there is no guarantee whether the signal will be unprocessed or not in that case.

- Set the output file format using [setOutputFormat()](https://developer.android.com/reference/android/media/MediaRecorder#setOutputFormat\(int\)). Note that starting with Android 8.0 (API level 26) MediaRecorder supports the MPEG2\_TS format, which is useful for streaming:

  [Kotlin](https://developer.android.com/media/platform/mediarecorder#kotlin)[Java](https://developer.android.com/media/platform/mediarecorder#java)

  mediaRecorder.setOutputFormat(MediaRecorder.OutputFormat.MPEG\_2\_TS)

- Set the output file name using [setOutputFile()](https://developer.android.com/reference/android/media/MediaRecorder#setOutputFile\(java.io.File\)). You must specify a file descriptor that represents an actual file.
- Set the audio encoder using [setAudioEncoder()](https://developer.android.com/reference/android/media/MediaRecorder#setAudioEncoder\(int\)).
- Complete the initialization by calling [prepare()](https://developer.android.com/reference/android/media/MediaRecorder#prepare\(\)).

Start and stop the recorder by calling [start()](https://developer.android.com/reference/android/media/MediaRecorder#start\(\)) and [stop()](https://developer.android.com/reference/android/media/MediaRecorder#start\(\)) respectively.

When you are done with the MediaRecorder instance free its resources as soon as possible by calling [release()](https://developer.android.com/reference/android/media/MediaRecorder#release\(\)).

**Note:** On devices running Android 9 (API level 28) or higher, apps running in the background cannot access the microphone. Therefore, your app should record audio only when it's in the foreground or when you include an instance of **MediaRecorder** in a [foreground service](https://developer.android.com/guide/components/services#Foreground).

**Using MediaMuxer to record multiple channels**

Starting with Android 8.0 (API level 26) you can use a [MediaMuxer](https://developer.android.com/reference/android/media/MediaMuxer) to record multiple simultaneous audio and video streams. In earlier versions of Android you can only record one audio track and/or one video track at a time.

Use the [addTrack()](https://developer.android.com/reference/android/media/MediaMuxer#addTrack\(android.media.MediaFormat\)) method to mix multiple tracks together.

You can also add one or more metadata tracks with custom information for each frame, but only to MP4 containers. Your app defines the format and content of the metadata.

**Adding metadata**

Metadata can be useful for offline processing. For example, data captured from the gyro sensor could be used to perform video stabilization.

When you add a metadata track, the track's mime format must start with the prefix application/. Writing metadata is the same as writing video or audio data, except that the data does not come from a MediaCodec. Instead, the app passes a ByteBuffer with an associated timestamp to the [writeSampleData()](https://developer.android.com/reference/android/media/MediaMuxer#writeSampleData\(int,%20java.nio.ByteBuffer,%20android.media.MediaCodec.BufferInfo\)) method. The timestamp must be in the same time base as the video and audio tracks.

The generated MP4 file uses the TextMetaDataSampleEntry defined in section 12.3.3.2 of the [ISO BMFF](https://en.wikipedia.org/wiki/ISO_base_media_file_format) specification to signal the metadata's mime format. When you use a [MediaExtractor](https://developer.android.com/reference/android/media/MediaExtractor) to extract a file that contains metadata tracks, the metadata's mime format appears as an instance of [MediaFormat](https://developer.android.com/reference/android/media/MediaFormat).

**Sample code**

The [MediaRecorder](https://github.com/android/media-samples/tree/main/MediaRecorder/) sample demonstrates how to make a video recording using MediaRecorder and the Camera API.

The example activity below shows how to use MediaRecorder to record an audio file. It Also uses MediaPlayer to play the audio back.

[Kotlin](https://developer.android.com/media/platform/mediarecorder#kotlin)[Java](https://developer.android.com/media/platform/mediarecorder#java)

package com.android.audiorecordtest

import android.Manifest
import android.content.Context
import android.content.pm.PackageManager
import android.media.MediaPlayer
import android.media.MediaRecorder
import android.os.Bundle
import android.support.v4.app.ActivityCompat
import android.support.v7.app.AppCompatActivity
import android.util.Log
import android.view.View.OnClickListener
import android.view.ViewGroup
import android.widget.Button
import android.widget.LinearLayout
import java.io.IOException

private const val LOG\_TAG = "AudioRecordTest"
private const val REQUEST\_RECORD\_AUDIO\_PERMISSION = 200

class AudioRecordTest : AppCompatActivity() {

`    `private var fileName: String = ""

`    `private var recordButton: RecordButton? = null
`    `private var recorder: MediaRecorder? = null

`    `private var playButton: PlayButton? = null
`    `private var player: MediaPlayer? = null

`    `// Requesting permission to RECORD\_AUDIO
`    `private var permissionToRecordAccepted = false
`    `private var permissions: Array<String> = arrayOf(Manifest.permission.RECORD\_AUDIO)

`    `override fun onRequestPermissionsResult(
`            `requestCode: Int,
`            `permissions: Array<String>,
`            `grantResults: IntArray
`    `) {
`        `super.onRequestPermissionsResult(requestCode, permissions, grantResults)
`        `permissionToRecordAccepted = if (requestCode == REQUEST\_RECORD\_AUDIO\_PERMISSION) {
`            `grantResults[0] == PackageManager.PERMISSION\_GRANTED
`        `} else {
`            `false
`        `}
`        `if (!permissionToRecordAccepted) finish()
`    `}

`    `private fun onRecord(start: Boolean) = if (start) {
`        `startRecording()
`    `} else {
`        `stopRecording()
`    `}

`    `private fun onPlay(start: Boolean) = if (start) {
`        `startPlaying()
`    `} else {
`        `stopPlaying()
`    `}

`    `private fun startPlaying() {
`        `player = MediaPlayer().apply {
`            `try {
`                `setDataSource(fileName)
`                `prepare()
`                `start()
`            `} catch (e: IOException) {
`                `Log.e(LOG\_TAG, "prepare() failed")
`            `}
`        `}
`    `}

`    `private fun stopPlaying() {
`        `player?.release()
`        `player = null
`    `}

`    `private fun startRecording() {
`        `recorder = MediaRecorder().apply {
`            `setAudioSource(MediaRecorder.AudioSource.MIC)
`            `setOutputFormat(MediaRecorder.OutputFormat.THREE\_GPP)
`            `setOutputFile(fileName)
`            `setAudioEncoder(MediaRecorder.AudioEncoder.AMR\_NB)

`            `try {
`                `prepare()
`            `} catch (e: IOException) {
`                `Log.e(LOG\_TAG, "prepare() failed")
`            `}

`            `start()
`        `}
`    `}

`    `private fun stopRecording() {
`        `recorder?.apply {
`            `stop()
`            `release()
`        `}
`        `recorder = null
`    `}

`    `internal inner class RecordButton(ctx: Context) : Button(ctx) {

`        `var mStartRecording = true

`        `var clicker: OnClickListener = OnClickListener {
`            `onRecord(mStartRecording)
`            `text = when (mStartRecording) {
`                `true -> "Stop recording"
`                `false -> "Start recording"
`            `}
`            `mStartRecording = !mStartRecording
`        `}

`        `init {
`            `text = "Start recording"
`            `setOnClickListener(clicker)
`        `}
`    `}

`    `internal inner class PlayButton(ctx: Context) : Button(ctx) {
`        `var mStartPlaying = true
`        `var clicker: OnClickListener = OnClickListener {
`            `onPlay(mStartPlaying)
`            `text = when (mStartPlaying) {
`                `true -> "Stop playing"
`                `false -> "Start playing"
`            `}
`            `mStartPlaying = !mStartPlaying
`        `}

`        `init {
`            `text = "Start playing"
`            `setOnClickListener(clicker)
`        `}
`    `}

`    `override fun onCreate(icicle: Bundle?) {
`        `super.onCreate(icicle)

`        `// Record to the external cache directory for visibility
`        `fileName = "${externalCacheDir.absolutePath}/audiorecordtest.3gp"

`        `ActivityCompat.requestPermissions(this, permissions, REQUEST\_RECORD\_AUDIO\_PERMISSION)

`        `recordButton = RecordButton(this)
`        `playButton = PlayButton(this)
`        `val ll = LinearLayout(this).apply {
`            `addView(recordButton,
`                    `LinearLayout.LayoutParams(
`                            `ViewGroup.LayoutParams.WRAP\_CONTENT,
`                            `ViewGroup.LayoutParams.WRAP\_CONTENT,
`                            `0f))
`            `addView(playButton,
`                    `LinearLayout.LayoutParams(
`                            `ViewGroup.LayoutParams.WRAP\_CONTENT,
`                            `ViewGroup.LayoutParams.WRAP\_CONTENT,
`                            `0f))
`        `}
`        `setContentView(ll)
`    `}

`    `override fun onStop() {
`        `super.onStop()
`        `recorder?.release()
`        `recorder = null
`        `player?.release()
`        `player = null
`    `}
}

