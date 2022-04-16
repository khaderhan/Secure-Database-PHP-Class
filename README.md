# Secure Database PHP Class

A PHP MySQL database client class to simplify database access.

This lightweight database class is written with PHP and uses the MySQLi extension, it uses prepared statements to
properly secure your queries, no need to worry about SQL injection attacks.

The MySQLi extension has built-in prepared statements that you can work with, this will prevent SQL injection and
prevent your database from being exposed, some developers are confused on how to use these methods correctly so I've
created this easy to use database class that'll do the work for you.

This database class is beginner-friendly and easy to implement, with the native MySQLi methods you need to write 3-7
lines of code to retrieve data from a database, with this class you can do it with just 1-2 lines of code, and is much
easier to understand.


# Let's Start!

The database class uses the MySQLi extension, this is built into PHP version >= 5.0.0. If you're using PHP version 5.0.0 to 5.3.0 you'll need install: mysqlnd.

No need to prepare statements using this class, it'll do that for you automatically (write less, do more), your queries will be secure, just remember to make sure you escape your output using `htmlspecialchars` PHP function, or your preferred escaping method.

PS: The transactions query aren't yet supported on this class.

# How To Use

## Download the source file

Download the file `db.php`. It contains the client PHP class named `db`.


## Connect to MySQL database:

```php
include 'db.php';

$dbhost = 'localhost';
$dbuser = 'root';
$dbpass = '';
$dbname = 'example';

$db = new db($dbhost, $dbuser, $dbpass, $dbname); // or update the default values of the parameters in db.php
```

## Fetch a record from a database:

```php
$account = $db->query('SELECT * FROM accounts WHERE username = ? AND password = ?', 'test', 'test')->fetchArray();
echo $account['name'];
```

Or you could do:

```php
$account = $db->query('SELECT * FROM accounts WHERE username = ? AND password = ?', array('test', 'test'))->fetchArray();
echo $account['name'];
```

## Fetch multiple records from a database:

```php
$accounts = $db->query('SELECT * FROM accounts')->fetchAll();

foreach ($accounts as $account) {
	echo $account['name'] . '<br>';
}
```

You can specify a callback if you do not want the results being stored in an array (useful for large amounts of data):

```php
$db->query('SELECT * FROM accounts')->fetchAll(function($account) {
    echo $account['name'];
});
```

If you need to break the loop you can add:

```php
return 'break';
```

## Update a record:

```php
$Update_Password = $db->query('UPDATE accounts SET password = ? WHERE username = ?', 'newpass', 'test');
```

And you can check if the action was success or fail by doing the following:
```php
if($Update_Password) {
    // Success
} else {
    // Failure
}
```

## Get the number of rows:

```php
$accounts = $db->query('SELECT * FROM accounts');
echo $accounts->numRows();
```

## Get the affected number of rows:

```php
$insert = $db->query('INSERT INTO accounts (username,password,email,name) VALUES (?,?,?,?)', 'test', 'test', 'test@gmail.com', 'Test');
echo $insert->affectedRows();
```

## Get the total number of queries:

```php
echo $db->query_count;
```

## Get the last insert ID:

```php
echo $db->lastInsertID();
```

## Close the database:

```php
$db->close();
```

# Disclaimer

The original class was published by David Adams on 2020-03-05 at https://codeshack.io/super-fast-php-mysql-database-class/ under the MIT license.

I brought it here to Github in order to improve it with the help of anybody that is interested in this piece of code.
If you find bugs or want to improve the code, please create an issue or pull request. Thanks.
