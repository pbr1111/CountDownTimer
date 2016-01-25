# CountDownTimer
Custom implementation of Android's CountDownTimer 

## Differences over the original implementation
* New empty constructor and `start(long millisInFuture, long countDownInterval)` method to change the `onTick(long millisUntilFinished)` interval and the time until the countdown is done. 
* Static handler class to prevent memory leaks. 

More information about handler's memory leaks can be found in:
- https://techblog.badoo.com/blog/2014/08/28/android-handler-memory-leaks/
- http://www.androiddesignpatterns.com/2013/01/inner-class-handler-memory-leak.html


## Android 
Also you can cherry-pick my commit (https://github.com/pbr1111/platform_frameworks_base/commit/4e093d4c450ecdcc1e8830a104379c80d2ea1df6), fixing the memory leak in the android/platform/frameworks/base project. This commit it's based on the original implementation and does not include the new contructor and start method. 

- Video of the original implementation: https://youtu.be/xueSSv8JaOY
- Video with the fixed version: https://youtu.be/DDMrR61CQLg


In the first video, it can be see the original implementation of the class CountDownTimer.java, using a anonymous handler class. 

When I rotate the device, MainActivity is destroyed and another instance is created. MainActivity.onCreate(Bundle) is called every time, creating another instance of the CountDownTimer class and it assigns this instance in the variable countDownTimer.

If I force the GC process, in theory the previous referenced instances of the CountDownTimer should be destroyed (nobody references this instances).

In the original implementation, this does not work this way, because the handler have a reference of the outer class. This causes a memory leak.

With the fixed implementation (static handler class), although if I destroy and recreate many times MainActivity, when I force the GC, unreferenced instances will be destroyed.

