# CountDownTimer
Custom implementation of Android's CountDownTimer 

## Differences over the original implementation
* New empty constructor and start(long millisInFuture, long countDownInterval) method to change the interval CountDown and the time until the countdown is done. 
* Static handler class to prevent memory leaks. 

More information about handler's memory leaks can be found in:
https://techblog.badoo.com/blog/2014/08/28/android-handler-memory-leaks/
http://www.androiddesignpatterns.com/2013/01/inner-class-handler-memory-leak.html
