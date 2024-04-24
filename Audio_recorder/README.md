Audio Recorder in Android with Example
Last Updated : 26 Dec, 2022
In Android for recording audio or video, there is a built-in class called MediaRecorder. This class in Android helps to easily record video and audio files. The Android multimedia framework provides built-in support for capturing and encoding common audio and video formats. In android for recording audio, we will use a device microphone along with MediaRecorder Class and for recording video, we will use the user’s device Camera and MediaRecorder Class. Now in this article, we will see the implementation of an audio recorder in Android with an example. 

Important Methods of MediaRecorder Class
Method 

Description

setAudioSource()	This method will specify the source of the audio to be recorded.
setAudioEncoder()	This method is used to specify the audio encoder.
setOutputFormat()	This method is used to specify the output format of our audio.
setOutputFile()	This method is used to specify the path of recorded audio files that are to be stored.
stop()	This method is used to stop the recording process. 
start()	This method is used to start the recording process. 
release()	This method is used to release the resource that is associated with the Media recorder class.
Example
Now we are creating a simple audio recorder app in which we will record audio from users device microphone and then we will store this audio recording in users device. We will also play this saved audio recording. A sample GIF is given below to get an idea about what we are going to do in this article. Note that we are going to implement this project using the Java language. 

Audio Recorder in Android 

Step by Step Implementation
Step 1: Create a New Project

To create a new project in Android Studio please refer to How to Create/Start a New Project in Android Studio. Note that select Java as the programming language. 

Step 2: Add permissions in the AndroidManifest.xml file

Add below line in the AndroidManifest.xml file. 

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.gtappdevelopers.camviewlibrary">
 
    <!--Permission for recording audio and storage of audio in users device-->
    <uses-permission android:name="android.permission.RECORD_AUDIO"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.STORAGE"/>
 
 
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.CamViewLibrary">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
 
</manifest>
Step 3: Modify the colors.xml and strings.xml file

Below is the code for the colors.xml file. 

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#0F9D58</color>
    <color name="purple_500">#0F9D58</color>
    <color name="purple_700">#0F9D58</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="gray">#A39696</color>
</resources>
Below is the code for the strings.xml file. 

<resources>
    <string name="app_name">GFG APP</string>
    <string name="toggle_flash">Toggle Flash</string>
    <string name="action_settings">Settings</string>
    <string name="scanned_data">Scanned Data</string>
    <string name="audio_recorder">Audio Recorder</string>
    <string name="start_recording">Start Recording</string>
    <string name="stop_recording">Stop Recording</string>
    <string name="play_recording">Play Recording</string>
    <string name="stop_playing">Stop Playing</string>
    <string name="status">Status</string>
</resources>
Step 4: Working with the activity_main.xml file

Navigate to the app > res > layout > activity_main.xml. Below is the code for the activity_main.xml file. Comments are added inside the code to understand the code in more detail. 

<?xml version="1.0" encoding="utf-8"?>
<!--XML code for activity_main.xml-->
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal"
    tools:context=".MainActivity">
 
    <!--Heading Text View-->
    <TextView
        android:id="@+id/txthead"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:text="@string/audio_recorder"
        android:textAlignment="center"
        android:textColor="@color/black"
        android:textSize="30sp" />
 
    <!--This will display the status of our app when 
        we will record some audio and play that audio-->
    <TextView
        android:id="@+id/idTVstatus"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="150dp"
        android:text="@string/status"
        android:textAlignment="center"
        android:textSize="18sp" />
 
    <!--Linear Layout for adding textviews
        in horizontal manner-->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:layout_marginTop="30dp"
        android:orientation="horizontal"
        android:weightSum="4">
 
        <!--Textview to start audio recording
            drawableTop will add above mic image-->
        <TextView
            android:id="@+id/btnRecord"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_margin="5dp"
            android:layout_weight="1"
            android:background="@color/purple_500"
            android:padding="5dp"
            android:text="@string/start_recording"
            android:textAlignment="center"
            android:textColor="@color/white"
            app:drawableTopCompat="@drawable/ic_start_recording" />
 
        <!--Textview to stop audio recording
            drawableTop will add above mic image-->
        <TextView
            android:id="@+id/btnStop"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_margin="5dp"
            android:layout_weight="1"
            android:background="@color/purple_500"
            android:padding="5dp"
            android:text="@string/stop_recording"
            android:textAlignment="center"
            android:textColor="@color/white"
            app:drawableTopCompat="@drawable/ic_stop_recording" />
 
        <!--Textview to play audio that is recorded
            drawableTop will add above mic image-->
        <TextView
            android:id="@+id/btnPlay"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_margin="5dp"
            android:layout_weight="1"
            android:background="@color/purple_500"
            android:padding="5dp"
            android:text="@string/play_recording"
            android:textAlignment="center"
            android:textColor="@color/white"
            app:drawableTopCompat="@drawable/ic_play_audio" />
 
        <!--Textview to pause the play of audio recording
            drawableTop will add above mic image-->
        <TextView
            android:id="@+id/btnStopPlay"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_margin="5dp"
            android:layout_weight="1"
            android:background="@color/purple_500"
            android:lines="2"
            android:padding="5dp"
            android:text="@string/stop_playing"
            android:textAlignment="center"
            android:textColor="@color/white"
            app:drawableTopCompat="@drawable/ic_pause_audio" />
 
    </LinearLayout>
</RelativeLayout>
Step 5: Working with the MainActivity.java file

Navigate to the app > java > Your app’s package name > MainActivity.java. Below is the code for the MainActivity.java file. Comments are added inside the code to understand the code in more detail. 

import android.content.pm.PackageManager;
import android.media.MediaPlayer;
import android.media.MediaRecorder;
import android.os.Bundle;
import android.os.Environment;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;
 
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
 
import java.io.IOException;
 
import static android.Manifest.permission.RECORD_AUDIO;
import static android.Manifest.permission.WRITE_EXTERNAL_STORAGE;
 
public class MainActivity extends AppCompatActivity {
 
    // Initializing all variables..
    private TextView startTV, stopTV, playTV, stopplayTV, statusTV;
     
    // creating a variable for media recorder object class.
    private MediaRecorder mRecorder;
     
    // creating a variable for mediaplayer class
    private MediaPlayer mPlayer;
     
    // string variable is created for storing a file name
    private static String mFileName = null;
     
    // constant for storing audio permission
    public static final int REQUEST_AUDIO_PERMISSION_CODE = 1;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
         
        // initialize all variables with their layout items.
        statusTV = findViewById(R.id.idTVstatus);
        startTV = findViewById(R.id.btnRecord);
        stopTV = findViewById(R.id.btnStop);
        playTV = findViewById(R.id.btnPlay);
        stopplayTV = findViewById(R.id.btnStopPlay);
        stopTV.setBackgroundColor(getResources().getColor(R.color.gray));
        playTV.setBackgroundColor(getResources().getColor(R.color.gray));
        stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));
 
        startTV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // start recording method will 
                // start the recording of audio.
                startRecording();
            }
        });
        stopTV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // pause Recording method will 
                // pause the recording of audio.
                pauseRecording();
 
            }
        });
        playTV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // play audio method will play 
                // the audio which we have recorded
                playAudio();
            }
        });
        stopplayTV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // pause play method will 
                // pause the play of audio
                pausePlaying();
            }
        });
    }
 
    private void startRecording() {
        // check permission method is used to check
        // that the user has granted permission 
        // to record and store the audio.
        if (CheckPermissions()) {
             
            // setbackgroundcolor method will change
            // the background color of text view.
            stopTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
            startTV.setBackgroundColor(getResources().getColor(R.color.gray));
            playTV.setBackgroundColor(getResources().getColor(R.color.gray));
            stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));
            
            // we are here initializing our filename variable
            // with the path of the recorded audio file.
            mFileName = Environment.getExternalStorageDirectory().getAbsolutePath();
            mFileName += "/AudioRecording.3gp";
             
            // below method is used to initialize 
            // the media recorder class
            mRecorder = new MediaRecorder();
             
            // below method is used to set the audio 
            // source which we are using a mic.
            mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);
             
            // below method is used to set 
            // the output format of the audio.
            mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP);
             
            // below method is used to set the 
            // audio encoder for our recorded audio.
            mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB);
             
            // below method is used to set the 
            // output file location for our recorded audio
            mRecorder.setOutputFile(mFileName);
            try {
                // below method will prepare
                // our audio recorder class
                mRecorder.prepare();
            } catch (IOException e) {
                Log.e("TAG", "prepare() failed");
            }
            // start method will start 
            // the audio recording.
            mRecorder.start();
            statusTV.setText("Recording Started");
        } else {
            // if audio recording permissions are
            // not granted by user below method will
            // ask for runtime permission for mic and storage.
            RequestPermissions();
        }
    }
 
    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        // this method is called when user will
        // grant the permission for audio recording.
        switch (requestCode) {
            case REQUEST_AUDIO_PERMISSION_CODE:
                if (grantResults.length > 0) {
                    boolean permissionToRecord = grantResults[0] == PackageManager.PERMISSION_GRANTED;
                    boolean permissionToStore = grantResults[1] == PackageManager.PERMISSION_GRANTED;
                    if (permissionToRecord && permissionToStore) {
                        Toast.makeText(getApplicationContext(), "Permission Granted", Toast.LENGTH_LONG).show();
                    } else {
                        Toast.makeText(getApplicationContext(), "Permission Denied", Toast.LENGTH_LONG).show();
                    }
                }
                break;
        }
    }
 
    public boolean CheckPermissions() {
        // this method is used to check permission
        int result = ContextCompat.checkSelfPermission(getApplicationContext(), WRITE_EXTERNAL_STORAGE);
        int result1 = ContextCompat.checkSelfPermission(getApplicationContext(), RECORD_AUDIO);
        return result == PackageManager.PERMISSION_GRANTED && result1 == PackageManager.PERMISSION_GRANTED;
    }
 
    private void RequestPermissions() {
        // this method is used to request the
        // permission for audio recording and storage.
        ActivityCompat.requestPermissions(MainActivity.this, new String[]{RECORD_AUDIO, WRITE_EXTERNAL_STORAGE}, REQUEST_AUDIO_PERMISSION_CODE);
    }
 
 
    public void playAudio() {
        stopTV.setBackgroundColor(getResources().getColor(R.color.gray));
        startTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
        playTV.setBackgroundColor(getResources().getColor(R.color.gray));
        stopplayTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
         
        // for playing our recorded audio
        // we are using media player class.
        mPlayer = new MediaPlayer();
        try {
            // below method is used to set the
            // data source which will be our file name
            mPlayer.setDataSource(mFileName);
             
            // below method will prepare our media player
            mPlayer.prepare();
             
            // below method will start our media player.
            mPlayer.start();
            statusTV.setText("Recording Started Playing");
        } catch (IOException e) {
            Log.e("TAG", "prepare() failed");
        }
    }
 
    public void pauseRecording() {
        stopTV.setBackgroundColor(getResources().getColor(R.color.gray));
        startTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
        playTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
        stopplayTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
         
        // below method will stop 
        // the audio recording.
        mRecorder.stop();
         
        // below method will release 
        // the media recorder class.
        mRecorder.release();
        mRecorder = null;
        statusTV.setText("Recording Stopped");
    }
 
    public void pausePlaying() {
        // this method will release the media player
        // class and pause the playing of our recorded audio.
        mPlayer.release();
        mPlayer = null;
        stopTV.setBackgroundColor(getResources().getColor(R.color.gray));
        startTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
        playTV.setBackgroundColor(getResources().getColor(R.color.purple_200));
        stopplayTV.setBackgroundColor(getResources().getColor(R.color.gray));
        statusTV.setText("Recording Play Stopped");
    }
}
All drawables are stored in the drawable folder. Navigate to the app > res > drawable folder to see all drawables. Now run the app on the Physical device to test it.  

Output: Run on Physical Device
Video Player
