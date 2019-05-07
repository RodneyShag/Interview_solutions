I found this code somewhere online.

### Solution

```java
class MyThread extends Thread {
    private String method;
    private CallInOrder foo;

    public MyThread(CallInOrder foo, String method) {
        this.method = method;
        this.foo = foo;
    }

    @Override
    public void run() {
        if (method == "first") {
            foo.first();
        } else if (method == "second") {
            foo.second();
        } else if (method == "third") {
            foo.third();
        }
    }
}
```


```java
class CallInOrder {
    public int pauseTime = 1000;
    public Semaphore sem1;
    public Semaphore sem2;

    public CallInOrder() {
        try {
            sem1 = new Semaphore(1); // Still unclear why we HAVE to use a semaphore here and can't use normal lock.
            sem2 = new Semaphore(1);

            sem1.acquire();
            sem2.acquire();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public void first() {
        try {
            System.out.println("Started Executing 1");
            Thread.sleep(pauseTime);
            System.out.println("Finished Executing 1");
            sem1.release();
        } catch (Exception ex) {
            ex.printStackTrace();
        }
    }

    public void second() {
        try {
            sem1.acquire();
            sem1.release();
            System.out.println("Started Executing 2");
            Thread.sleep(pauseTime);
            System.out.println("Finished Executing 2");
            sem2.release();
        } catch (Exception ex) {
            ex.printStackTrace();
        }
    }

    public void third() {
        try {
            sem2.acquire();
            sem2.release();
            System.out.println("Started Executing 3");
            Thread.sleep(pauseTime);
            System.out.println("Finished Executing 3");
        } catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```
