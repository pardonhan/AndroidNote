# Android相册应用
## 第一步 获取手机图片
	获取手机图片，首先要去遍历手机的文件夹，获取到有图片的文件，这肯定是一个耗时的操作。
	耗时操作就需要有一个线程来完成。
	使用ExecutorService线程池来完成这一操作。

### ExecutorService线程池的使用

```java
// 单例线程，表示在任意的时间段内，线程池中只有一个线程在工作...
ExecutorService executorService = Executors.newSingleThreadExecutor();
```

```java
// 
ExecutorService executorService = Executors.newFixedThreadPool(10);
```

```java
// 
ExecutorService executorService = Executors.newScheduledThreadPool(10);
```

```java
/** 
 * 缓存线程池，先查看线程池中是否有当前执行线程的缓存，如果有就resue(复用),
 * 如果没有,那么需要创建一个线程来完成当前的调用.并且这类线程池只能完成一些生存期很短的一些任务.
 * 并且这类线程池内部规定能resue(复用)的线程，空闲的时间不能超过60s,一旦超过了60s,就会被移出线程池.
 */
ExecutorService executorService = Executors.newCacheThreadPool();
```