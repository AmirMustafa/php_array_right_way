# php_array_right_way
PHP - Working with PHP Array Right Ways

Here I am going to make a list of common PHP array functions with examples of usage and best practices.
Every PHP developer must know how to use them and how to combine array functions to make code readable and
short.

<br><br>
## The Basics
<b>1.	array_combine()</b><br>
Let's start with the basic functions that work with array keys and values. One of them is array_combine(), which creates an array using one array for keys and another for its values:<br>

```
$keys = ['sky', 'grass', 'orange'];
$values = ['blue', 'green', 'orange'];
 
$array = array_combine($keys, $values);
print_r($array);
 
// Array
// (
//     [sky] => blue
//     [grass] => green
//     [orange] => orange
// )

```

<b>2.	array_values()</b><br>

Let's start with the basic functions that work with array keys and values. One of them is array_combine(), which creates an array using one array for keys and another for its values:<br>

```
	print_r(array_keys($array)); // ['sky', 'grass', 'orange'];
```

<b>3. array_keys()</b><br>

Gives the array of keys leaving keys in numeric array style<br>

```
	print_r(array_values($array)); // ['blue', 'green', 'orange'];
```

<b>4.	array_flip()</b><br>

keys turns into value and vice versa

```
	print_r(array_flip($array));
 
// Array
// (
//     [blue] => sky
//     [green] => grass
//     [orange] => orange
// )

```
## Make your code shorter:
a. When  we have array and want to store each index value in a variable, list()
Is important<br>
b. The function list(), which is not really a function, but a language construction, is designed to assign variables in a short way. For example, here is a basic example of using the list() function:<br>

<b>5.	List()</b><br>

keys turns into value and vice versa

```
	// define array
$array = ['a', 'b', 'c'];
 
// without list()
$a = $array[0];
$b = $array[1];
$c = $array[2];		// no. of parameter = no. of lines
 
// with list()
list($a, $b, $c) = $array;	// in one line


```

c. list () also works best with functions like preg_slit() or explode() <br>
```
<?php 
$date = '12-08-2018';
list($dd, $mm, $yy) = explode('-', $date);
echo $dd;		//12

```

d.list() also works well with foreach
```
<?php 
$arrays = [[1, 2], [3, 4], [5, 6]];
foreach ($arrays as list($a, $b)) {
	
    $c = $a + $b;
    echo($c . ', '); // 3, 7, 11, 	- each array values added
}

```
<b>6.	extract()</b><br>
a. works only for associative array<br>
b. converts associative array to variables

```
<?php
$array = [
    'clothes' => 't-shirt',
    'size'    => 'medium',
    'color'   => 'blue',
];
 
extract($array);
 
echo("$clothes $size $color"); // t-shirt medium blue

```


