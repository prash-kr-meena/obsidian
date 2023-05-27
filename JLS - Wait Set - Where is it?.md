**Stack Overflow** [JLS - Wait Set - Where is it?](https://stackoverflow.com/questions/53633839/jls-wait-set-where-is-it)

---

The JLS for Java SE 11 Edition says in [chapter 17.2](https://docs.oracle.com/javase/specs/jls/se11/html/jls-17.html#jls-17.2):

> Every object, in addition to having an associated monitor, has an associated _wait set_. A wait set is a set of threads.
> 
> When an object is first created, its wait set is empty.

The [documentation](https://docs.oracle.com/javase/10/docs/api/java/lang/Object.html#wait(long,int)) of `Object.wait` says:

> This method causes the current thread (referred to here as _T_) to place itself in the wait set for this object [...]
> 
> The thread _T_ is then removed from the wait set for this object [...]

Where is this _wait set_ located?

The wording "has an associated _wait set_" and "wait set for this object" indicates it's not part of an object. And as far I can see it's not mentioned by the [`class` File Format](https://docs.oracle.com/javase/specs/jvms/se11/html/jvms-4.html) of the JVM.

Is the _wait set_ not part of the JVM? Is it part of the OS, i.e. the thread scheduler?

Is there an API to read the _wait set_ (i.e. for monitoring purposes)? Something like `ThreadInfo` returned by `ThreadMXBean`?

---
The wait set mentioned in the Java Language Specification (JLS) is not directly accessible through the Java API. It represents a conceptual construct associated with each object in Java, but its implementation details are not specified in the JLS.

The wait set is maintained by the JVM (Java Virtual Machine) and is typically implemented by the underlying operating system's thread scheduler. It is used to manage threads that are waiting for a particular object's monitor.

Although there is no direct API provided to access or manipulate the wait set, you can obtain some information related to thread synchronization and wait sets through the `ThreadMXBean` interface in the `java.lang.management` package. The `ThreadMXBean` interface provides methods to monitor and manage threads in a Java application, including information about thread states, thread contention, and synchronization.

For example, you can use the `ThreadMXBean.getThreadInfo()` method to retrieve `ThreadInfo` objects, which provide information about a particular thread's state, including whether it is in a waiting state.

Here's an example of using `ThreadMXBean` to get thread information:

```java
import java.lang.management.ManagementFactory;
import java.lang.management.ThreadInfo;
import java.lang.management.ThreadMXBean;

public class ThreadInfoExample {
    public static void main(String[] args) {
        ThreadMXBean threadMXBean = ManagementFactory.getThreadMXBean();
        long[] threadIds = threadMXBean.getAllThreadIds();
        ThreadInfo[] threadInfos = threadMXBean.getThreadInfo(threadIds);

        for (ThreadInfo threadInfo : threadInfos) {
            // Access thread information, including state and synchronization details
            System.out.println(threadInfo.getThreadName() + ": " + threadInfo.getThreadState());
        }
    }
}
```

Keep in mind that the specific implementation and details of the wait set may vary across JVM implementations and operating systems. Therefore, the availability and level of information regarding the wait set may also vary.

For more information, you can refer to the Java SE 11 Edition of the Java Language Specification (JLS), Section 17.2:
- [Java Language Specification, Java SE 11 Edition, Section 17.2: Wait Sets and Notification](https://docs.oracle.com/javase/specs/jls/se11/html/jls-17.html#jls-17.2)

And for information on monitoring threads and synchronization, you can refer to the `ThreadMXBean` documentation:
- [Java Platform SE 11 API Specification: java.lang.management.ThreadMXBean](https://docs.oracle.com/en/java/javase/11/docs/api/java.management/java/lang/management/ThreadMXBean.html)
