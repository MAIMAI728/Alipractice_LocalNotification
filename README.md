# Local Notification
1st Presentation : Ali's class of Android

Check point:  
Please check sendNotification（） of MainActivity.java  
In this method I have defined Intent and PendingIntent object to redirect user to some activity when user touches the notification.

```private void sendNotification() {
      Intent notificationIntent = new Intent(this, MainActivity.class);
      PendingIntent contentIntent = PendingIntent.getActivity(this, 0, notificationIntent, PendingIntent.FLAG_UPDATE_CURRENT);
      notificationBuilder.setContentIntent(contentIntent);
      Notification notification = notificationBuilder.build();
      notification.flags |= Notification.FLAG_AUTO_CANCEL;
      notification.defaults |= Notification.DEFAULT_SOUND;
      currentNotificationID++;
      int notificationId = currentNotificationID;
      if (notificationId == Integer.MAX_VALUE - 1)
          notificationId = 0;
      notificationManager.notify(notificationId, notification);
  }
```
To assign some action when user touches the notification, I need to set PendingIntent object in `notificationBuilder.setContentIntent() method`.


--------------------------------------------------------------------------------
References:  

☆PendingIntent  
https://developer.android.com/reference/android/app/PendingIntent.html

☆NotificationCompat.Builder   
https://developer.android.com/reference/android/support/v4/app/NotificationCompat.Builder.html


--------------------------------------------------------------------------------

Notes:  

I didn't lecture about "changing priority of Notification" and "combinating Notification" at my presentation. Please follow with "//★add" of my code if you took my WS.

I changed :  
MainActivity.java  
activity_main.xml (just uncomment)


## Demo

★Simple Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/simpleNotification.gif)


★Expand Layout Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/ExpandLayoutNotification.gif)


★Notification With Action Button Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/actionNotification.gif)


★[New] Max Priority Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/MaxPriority.gif)


★[New] Min Priority Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/MinPriority.gif)


★[New] Combination Notification

![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/combinationNotification.gif)
