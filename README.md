# MyApplicationLightSensor

  # Sensor (Light Sensor)
  
  What is sensor? 

According to Google’s developer’s guide - Most Android powered devices have built-in sensors that measures motion, orientation and various environmental conditions.  Which monitor ambience, humidity, illuminance, ambience pressure, and ambience light near the device.  environment sensors are not always available on devices. Because of this, it’s particularly important that you verify at runtime whether an environment sensor exists before you attempt to acquire data from it. I will narrow this topic to illustrate one of the four environment sensors provided by Android platform which is Light sensor. 

Light sensor is used mostly by manufacturers to control screen brightness. I will be using a TextView control to display the information we will obtain from android light sensor.

Before we go into more details, it is important to understand what we are planning to achieve. So, by the end of this demo you will learn how to create a light sensor application. 

Below is a screenshot of the application we will create.
 
Let’s start creating our app, feel free to use whichever tools that works for you, but I am using are: -

Windows 10

Android Studio

Huawei Mate 10 lite

Creating an android project, follow these steps

Go to file menu

Click on New menu

Click Android project

Enter Project Name: MyApplicationLightSensor and click next

On Select form factor and minimum SDK window

Click on Phone/Tablet (it will give you a default API but you can choose whichever that your Device can handle) and click next

Select Blank Activity

Name the Activity LighSensorActivity

Keep other default selections

Continue to click on next button until Finish button is active, then click on Finish Button. 

Let’s start with our project.

Go to the res folder click on the layout folder We are going to create the main layout of our android app. Open the file activity_light_sensor.xml, copy and paste the code below inside the file.
  
    <?xml version="1.0" encoding="utf-8"?>

    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.yolly.myapplicationlightsensor.LightSensorActivity"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/app_name"
    tools:context=".LightsensorActivity" />

    <TextView
        android:id="@+id/lt_avai"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" /> 
  
    <TextView
        android:id="@+id/lt_reading"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"/>
    
    </LinearLayout>

For the Activity file, open LightSensorActivity file, we will get the instance of the TextView widget in the layout file. We will add the Sensor and SensorManager classes as variable in the Activity class.

    import android.hardware.Sensor;
    import android.hardware.SensorEvent;
    import android.hardware.SensorEventListener;
    import android.hardware.SensorManager;

Inside the onCreate(Bundle savedInstanceState) method of the Activity class, we will create the objects of the Sensor and SensorManager classes.

        SensorManager mySensorManager = (SensorManager)getSystemService(SENSOR_SERVICE);
        Sensor LightSensor = mySensorManager.getDefaultSensor(Sensor.TYPE_LIGHT);

Now open LightSensorActivity class, copy and paste the code inside the file.

    import android.support.v7.app.AppCompatActivity;
    import android.os.Bundle;
    import android.hardware.Sensor;
    import android.hardware.SensorEvent;
    import android.hardware.SensorEventListener;
    import android.hardware.SensorManager;
    import android.widget.TextView;

    public class LightSensorActivity extends AppCompatActivity {

    TextView lt_avai, lt_reading;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_light_sensor);

        lt_avai
                = (TextView)findViewById(R.id.lt_avai);
        lt_reading
                = (TextView)findViewById(R.id.lt_reading);
        SensorManager mySensorManager = (SensorManager)getSystemService(SENSOR_SERVICE);

        Sensor LightSensor = mySensorManager.getDefaultSensor(Sensor.TYPE_LIGHT);

        if (LightSensor != null) {
            lt_avai.setText("Sensor.TYPE_LIGHT Available");
            mySensorManager.registerListener(
                    LightSensorListener,
                    LightSensor,
                    SensorManager.SENSOR_DELAY_NORMAL);

        } else {
            lt_avai.setText("Sensor.TYPE_LIGHT NOT Available");
        }
    }

    private final SensorEventListener LightSensorListener
            = new SensorEventListener() {


      @Override
        public void onAccuracyChanged(Sensor sensor, int accuracy) {
         // TODO Auto-generated method stub

        }
        @Override
        public void onSensorChanged(SensorEvent event) {
            if (event.sensor.getType() == Sensor.TYPE_LIGHT) {
                lt_reading.setText("LIGHT: " + event.values[0]);

            }
        }

    };
}
 


This brings us to the end of this tutorial. I hope that you have learn something. Now build your application by clicking on the hammer icon on your tool bar and run your project.

#Evaluation 

Creating a light sensor went well just that I had to wait until the night falls to test if it can sense some light or not. 

#Conclusion

 I would recommend Light Sensors to others it is a cool feature to have on a device,  it can enable you to automatically control the light  /brightness on your device at night and you one will have eye friendly light when using their devices.







