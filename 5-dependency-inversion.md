# Dependency Inversion

> High level modules should not depend on low level modules.

> Depend on abstractions, not on concretions.

All of this is about **decoupling code**. If a code is hard to change, or you're reluctant to change it, it is badly designed.

## Code example - DB connection

```php
<?php
class PasswordReminder {

	private $dbConnection;

	// Why password reminder is aware of the MySQL connection?
	// It is a low level module
	public function __construct(MySQLConnection $dbConnection)
	{
		$this->dbConnection = $dbConnection;
	}
}

// We should do something like this
interface ConnectionInterface {
	public function connect();
}

class DbConnection implements ConnectionInterface {
	public function connect() {}
}

class PasswordReminder {

	private $dbConnection;

	public function __construct(ConnectionInterface $dbConnection)
	{
		$this->dbConnection = $dbConnection;
	}
}
?>
```