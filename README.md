# php_array_right_way
PHP - Working with PHP Array Right Ways

Here I am going to make a list of common PHP array functions with examples of usage and best practices.
Every PHP developer must know how to use them and how to combine array functions to make code readable and
short.

<br><br>
## The basics
<b>1.	array_combine()</b>
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




<b></b>
<b></b><b></b>
<b></b>
