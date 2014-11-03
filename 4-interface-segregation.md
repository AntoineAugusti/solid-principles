# Interface Segregation

> A client should not be forced to implement an interface that it doesn't use.


## Code example
```php 
<?php

// Such interface is not appropriate for an
// Android because it doesn't need to sleep
interface WorkerInterface {
	public function work();
	public function sleep();
}

// Instead, create small interfaces
interface Workable {
	public function work();
}

interface Sleepable {
	public function sleep();
}

interface ManageableInterface {
	public function beManaged();
}

class HumanWorker implements Workable, Sleepable, ManageableInterface {
	
	public function work() {}

	public function sleep() {}

	public function beManaged()
	{
		$this->work();
		$this->sleep();
	}
}

class AndroidWorker implements Workable, ManageableInterface {
	
	public function work() {}

	public function beManaged()
	{
		$this->work();
	}
}

class Captain {
	
	public function manage(ManageableInterface $worker)
	{
		// A bad practise would be to test the type of the worker
		// to know if we need to call another method
		$worker->beManaged();
	}
}
?>
```