This is the way I did, [Riddhi Dutta](https://youtu.be/WldMTtUWqTg?list=PL4WwUkr0wZURiHPaQDb-SwkY36QUAgc4p&t=6733) had created it in some other way



```java
  
public class Application {  
  
	public static void main(String[] args) throws InterruptedException {  
	System.out.println("hi");  
	  
	Queue queue = new Queue();  
	
	Thread thread1 = new Thread(() -> {  
		for (int i = 0; i < 15; i++) {  
			queue.setTrue();  
		}  
	}, "Thread1");  
	  
	Thread thread2 = new Thread(() -> {  
		for (int i = 0; i < 15; i++) {  
			queue.setFalse();  
		}  
	}, "Thread2");  
	  
	thread1.start();  
	thread2.start();  
	  
	}  
  
}  
  
  
class Queue {  
  
private Boolean flag_true = Boolean.TRUE;  
private Boolean flag_false = Boolean.FALSE;  
  
  
public void setTrue() {  
	synchronized (flag_true) {  
	while (flag_false == false) {  
		try {  
		flag_true.wait();  
		} catch (InterruptedException e) {  
		System.out.println("Exception in setTrue method");  
		throw new RuntimeException(e);  
		}
	}  
	System.out.println(Thread.currentThread().getName() + " Setting True Called");  
	System.out.println(Thread.currentThread().getName() + " Current Value : " + flag_true);  
	flag_true = true;  
	System.out.println(Thread.currentThread().getName() + " After Value : " + flag_true);  
	}  
}  
  
  
public void setFalse() {  
	synchronized (flag_false) {  
		while (flag_true == true) {  
		try {  
		flag_false.wait();  
		} catch (InterruptedException e) {  
		System.out.println("Exception in setFalse method");  
		throw new RuntimeException(e);  
		}  
	}  
	System.out.println(Thread.currentThread().getName() + " Setting False Called");  
	System.out.println(Thread.currentThread().getName() + " Current Value : " + flag_false);  
	flag_false = false;  
	System.out.println(Thread.currentThread().getName() + " After Value : " + flag_false);  
	}  
}  
  
}
```