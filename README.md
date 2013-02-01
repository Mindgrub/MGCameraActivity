MGCameraActivity
================

A picture taking activity that will return you the uri of a CORRECTLY oriented image

Due to the unpredictability of Android's camera activities this activity is written for you to take pictures
and will return a correctly oriented image.

This Activity can be started like any other activity, simply start it with a desired request code (which you will catch
in onActivityResult) and set the desired path for the image to be saved.  Here is an example use:

<pre>
private void startCameraActivity()
{
    //MGCameraActivity can be provided with a preferred filepath for the image, or will generate one if none is included in the extras
    Intent i = new Intent(activity, MGCameraActivity.class);
    i.putExtra(MGCameraActivity.IMAGE_FILE_PATH, activity.getCacheDir().getAbsolutePath() + "/" + String.valueOf(System.currentTimeMillis()));
    activity.startActivityForResult(i, CAMERA_PIC_REQUEST);
}

public void onActivityResult(int requestCode, int resultCode, Intent data)
{
    if(requestCode == CAMERA_PIC_REQUEST && resultCode == Activity.RESULT_OK)
    {
    	//if taken from camera, create uri from the included filepath
    	if(data != null && data.hasExtra(MGCameraActivity.IMAGE_FILE_PATH))
    		imageUri = Uri.parse("file://" + data.getStringExtra(MGCameraActivity.IMAGE_FILE_PATH));
    }
} 
</pre>
