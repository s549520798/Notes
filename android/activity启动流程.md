### Activity 启动流程

参考
[anroid源码在线查询地址](https://cs.android.com/?hl=zh-cn)

####1、 Launcher 启动应用

代码路径：packages/apps/Launcher3/src/com/android/launcher3/Launcher.java
step:
1.  Launcher.startActivitySafely(View v, Intent intent, ItemInfo item,
            @Nullable String sourceContainer)
    packages/apps/Launcher3/src/com/android/launcher3/BaseDraggingActivity.java
    BaseDraggingActivity.startActivitySafely()
2. Activity.startActivity(Intent intent, @Nullable Bundle options)
   Activity.startActivityForResult(Intent intent, int requestCode, Bundle options)
3. Instrumentation.execStartActivity(Context who, IBinder contextThread, IBinder token, Activity target, Intent intent, int requestCode, Bundle options) 
   路径 frameworks/base/core/java/android/app/Instrumentation.java
4. ActivityTaskManager.getService().startActivity
   IActivityTaskManager.startActivity() 
   获取系统service ServiceManager.getService(Context.ACTIVITY_TASK_SERVICE)执行startActivity
   IActivityTaskManager.sub的实现类 ActivityTaskManamgerService
5. ActivityTaskManagerService.startActivity()
   路径 frameworks/base/services/core/java/com/android/server/wm/ActivityTaskManagerService.java
   经过一系列复杂调用会到6
6. ActivityStackSupervisor.startSpecificActivity()

   ```java
   // Is this activity's application already running? 判断是否程序已经运行
    final WindowProcessController wpc =
            mService.getProcessController(r.processName, r.info.applicationInfo.uid);
    boolean knownToBeDead = false;
    if (wpc != null && wpc.hasThread()) {
        try {
            //如果已经运行，走这里创建Activity
            realStartActivityLocked(r, wpc, andResume, checkConfig);
            return;
        } catch (RemoteException e) {
            Slog.w(TAG, "Exception when starting activity "
                    + r.intent.getComponent().flattenToShortString(), e);
        }
        // If a dead object exception was thrown -- fall through to
        // restart the application.
        knownToBeDead = true;
    }

    r.notifyUnknownVisibilityLaunchedForKeyguardTransition();

    final boolean isTop = andResume && r.isTopRunningActivity();
    //如果之前Activity不存在，走这里创建进程
    mService.startProcessAsync(r, knownToBeDead, isTop, isTop ? "top-activity" : "activity");
   ```

   这里是很重要的一步, 判断了是否是应用内启动activity
7. ActivityManagerService#LoaclService.startProcess()
   ActivityManagerService#LoaclService.startProcessLocked()
8. Zygote 启动流程
9. Zygote 启动新的Process
10. 


####2、 应用内启动Activity