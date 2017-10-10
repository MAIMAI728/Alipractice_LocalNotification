# Local Notification
1st Presentation : Ali's class of Android

Check point:  
Please check sendNotification（） of MainActivity.java  
In this method I have defined Intent and PendingIntent object to redirect user to some activity when user touches the notification.

```
private void sendNotification() {
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
`NotificationCompat.Builder` is used to set notification icon, text, style, title and more.

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
```
private void setDataForSimpleNotification() {
        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setContentText(notificationText);
        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/simpleNotification.gif)


★Expand Layout Notification  
```
private void setDataForExpandLayoutNotification() {
        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(notificationText))
                .setContentText(notificationText);

        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/ExpandLayoutNotification.gif)


★Notification With Action Button Notification  
[!] Not recommended to use a device with wigh API(25 or 26) for checking icon images(thumbs_up, thumb_down). It looks easy to see with 22 API.  
```
private void setDataForNotificationWithActionButton() {

        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(notificationText))
                .setContentText(notificationText);

        Intent answerIntent = new Intent(this, AnswerReceiveActivity.class);
        answerIntent.setAction("Yes");
        PendingIntent pendingIntentYes = PendingIntent.getActivity(this, 1, answerIntent, PendingIntent.FLAG_UPDATE_CURRENT);
        notificationBuilder.addAction(R.drawable.thumbs_up, "Yes", pendingIntentYes);

        answerIntent.setAction("No");
        PendingIntent pendingIntentNo = PendingIntent.getActivity(this, 1, answerIntent, PendingIntent.FLAG_UPDATE_CURRENT);
        notificationBuilder.addAction(R.drawable.thumbs_down, "No", pendingIntentNo);
        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/actionNotification.gif)


★[New] Max Priority Notification  
PRIORITY_MAX  
---Use for critical and urgent notifications.  

```
private void setDataForMaxPriorityNotification() {
        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(notificationText))
                .setPriority(Notification.PRIORITY_MAX)
                .setContentText(notificationText);

        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/MaxPriority.gif)


★[New] Min Priority Notification  
PRIORITY_MIN  
---Use for contextual or background information notifications.  

```
private void setDataForMinPriorityNotification() {
        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(notificationText))
                .setPriority(Notification.PRIORITY_MIN)
                .setContentText(notificationText);

        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/MinPriority.gif)

--------------------------------------------------------------------------------
References:  

☆Notification.BigTextStyle  
https://developer.android.com/reference/android/app/Notification.BigTextStyle.html  

--------------------------------------------------------------------------------

★[New] Combination Notification  
When you see the simple notification, you can see "Title" and when you tap to see detail then you can see "detail Text" on the top!  

```
private void setDataForCombinedNotification() {
        combinedNotificationCounter++;
        notificationBuilder = new NotificationCompat.Builder(this)
                .setSmallIcon(R.mipmap.ic_launcher)
                .setLargeIcon(icon)
                .setContentTitle(notificationTitle)
                .setGroup("group_emails")
                .setGroupSummary(true)
                .setContentText(combinedNotificationCounter + " new messages");

        // This is detail box when you tap to see it.
        NotificationCompat.InboxStyle inboxStyle = new NotificationCompat.InboxStyle();
        inboxStyle.setBigContentTitle(notificationText);
        inboxStyle.setSummaryText("sample : test@gmail.com");
        //you can add 7 lines so far.
        //When notifications are combined, the counter would be increased too.
        for (int i = 0; i < combinedNotificationCounter; i++) {
            inboxStyle.addLine("This is Test " + i);
        }

        currentNotificationID = 500;
        notificationBuilder.setStyle(inboxStyle);
        sendNotification();
    }
```
![result](https://github.com/MAIMAI728/Alipractice_LocalNotification/blob/master/images/combinationNotification.gif)
