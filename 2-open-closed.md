# Open Closed

> Entities should be open for extension, but closed for modification.

A class should be easy to modify and, at the same time, we should be able to change behaviour without changing source code. It is obviously a goal, something we are aiming for.

## Good practices
- Separate extensible behaviour behind an interface and flip the dependencies.
- If you're trying to call a specific method based on the type of an object, you're doing something wrong.

## Code example - figures
```php
<?php
// Our contract that we will need to satisfy
interface Shape {
	public function area();
}

class Circle implements Shape {
	
	private $radius;

	function __construct($radius)
	{
		$this->radius = $radius;
	}

	public function area()
	{
		return $this->radius * $this->radius * pi();
	}
}

class Rectangle implements Shape {
	
	private $width;
	private $height;

	function __construct($width, $height)
	{
		$this->width = $width;
		$this->height = $height;
	}

	public function area()
	{
		return $this->height * $this->width;
	}
}

class AreaCalculator {

	public function calculate($shapes)
	{
		$area = [];

		foreach($shapes as $shape)
		{
			// Take advantage of the interface
			$area[] = $shape->area();
		}

		return array_sum($area);
	}
}
?>
```
## Code example - checkout
```php
<?php
interface PaymentMethodInterface {
	public function acceptPayment(Receipt $receipt);
}

class CashPayment implements PaymentMethodInterface {
	public function acceptPayment($receipt)
	{
		// The logic goes here
	}
}

class Checkout {
	public function begin(Receipt $receipt, PaymentMethodInterface $payment)
	{
		$payment->acceptPayment($receipt);
	}
}
?>
```