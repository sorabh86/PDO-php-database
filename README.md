# PDO Help Guide

## Print Available Drivers
```php
<?php

print_r(PDO::getAvailableDrivers());

```
## MSSQL
```php
<?php
$db = new PDO('dblib:host=your_hostname;dbname=your_db;charset=UTF-8', $user, $pass);

$db = new PDO('mssql:host=sqlserver;dbname=database', 'username',
'password');

$Stmt = $db->prepare('p_sel_all_termlength ?');
$Stmt->bindParam(1, $ErrorCode, PDO::PARAM_INT,4);
$Smt->execute();
echo "Error = ". $ErrorCode ."\n";

```
## Oracle
```php
<?php
try {
  $dbh = new PDO('odbc:SAMPLE', 'db2inst1', 'ibmdb2',
      array(PDO::ATTR_PERSISTENT => true));
....... 
} catch (Exception $e) {
  $dbh->rollBack();
  echo "Failed: " . $e->getMessage();
}

?> 
```
## MySQL
```php
<?php
// connecting
<?php
$dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);

// Handling connection errors
try {
    $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
    foreach($dbh->query('SELECT * from FOO') as $row) {
        print_r($row);
    }
    $dbh = null;
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

// persistent connection
$dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass, array(
    PDO::ATTR_PERSISTENT => true
));

// query
$sth = $dbh->query('SELECT * FROM foo');
$stmt->execute();

// execute with indexed array
$stmt = $dbh->prepare("SELECT * FROM REGISTRY where name LIKE '%?%'");
$stmt->execute(array($_GET['name']));

// execute with assoc array
$stmt = $dbh->prepare("SELECT * FROM REGISTRY where name LIKE '%:name%'");
$stmt->execute(array('name'=>$_GET['name']));

// bind params
$stmt = $dbh->prepare ("INSERT INTO user (firstname, surname) VALUES (:f-name, :s-name)");
$stmt -> bindParam('f-name', $fname);
$stmt -> bindParam('s-name', $sname);

$fname = 'John';
$sname = 'Smith';
$stmt -> execute();

$fname = 'Rock';
$sname = 'Jackson';
$stmt -> execute();

```
