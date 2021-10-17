PHP Tutorial: https://www.w3schools.com/php/default.asp

## Syntax
```php
<?php
echo "My first PHP script!";
?>
```
## Comments
```php
<?php
// This is a single-line comment
# This is also a single-line comment
/*
This is a multiple-lines comment block
that spans over multiple
lines
*/
?>
```
## Variables
```php
<?php
$txt = "Hello world!";
$x = 5;
?>
```

## Echo
```php
<?php
$txt1 = "Learn PHP";
$txt2 = "W3Schools.com";
$x = 5;
$y = 4;

echo "<h2>" . $txt1 . "</h2>";
echo "Study PHP at " . $txt2 . "<br>";
echo $x + $y;
?>
```

## Data types
```php
<?php
$a = "Hello world!"; // String
$b = 5985; //Integer
$c = 10.365; //Float
$x = true; //boolean
$y = false; //boolean
$x = null;
$cars = array("Volvo","BMW","Toyota");
?>
```

## Class
```php
<?php
class Car {
  public $color;
  public $model;
  public function __construct($color, $model) {
    $this->color = $color;
    $this->model = $model;
  }
  public function message() {
    return "My car is a " . $this->color . " " . $this->model . "!";
  }
}

$myCar = new Car("black", "Volvo");
echo $myCar -> message();
echo "<br>";
$myCar = new Car("red", "Toyota");
echo $myCar -> message();
?>
```

## Strings
