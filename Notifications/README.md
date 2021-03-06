# Notifications

## Creating a Notification


### Flags to control persistence of Notifications

Various flags are available that control the persistence of Notifications. 
* FLAG_AUTO_CANCEL
* FLAG_FOREGROUND_SERVICE
* FLAG_NO_CLEAR
* FLAG_ONGOING_EVENT

## Setting a content view for a Notification
The content view of a Notification is an instance of RemoteViews. 

The content view of a Notification is displayed when the notification is expanded.

When a Notificaiton's Builder is used to create a Notification, the Builder creates an appropriate content view using title and text and sets it on the notification.

However, the Content View (a RemoteViews instance) for a Notification can be set explicitly by
* Creating a layout file 
* Creating a RemoteViews instance by passing in the package name and the resource ID of the layout file as arguments
* Create the Notification object by calling *setContent()* on the *Notification.Builder* object prior to calling the *build()* method

### Valid RemoteViews Controls
* Button
* TextView
* ImageButton
* ImageView
* FrameLayout
* LinearyLayout
* RelativeLayout
* AnalogClock
* ProgressBar
* Chronometer





