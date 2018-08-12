# php_array_right_way
PHP - Working with PHP Array Right Ways

Here friends I am sharing some important PHP array functions came accross reading. These inbuilt functions are very powerful, I guess every PHP developer should have idea about.

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

<b>7. compact()</b><br>
a. converts variable to associative array, opp of above case

```
<?php
$clothes = 'jeans';
$size	 = 'medium';
$color	 = 'blue';

$array = compact('clothes', 'size', 'color');

echo '<pre>';
print_r($array);

// o/p
Array
(
    [clothes] => jeans
    [size] => medium
    [color] => blue
)


```
## Filtering Functions

<b>8. array_filter</b><br>
a. With callbacks: Filter positive or negative values

```
<?php
$numbers = [20, -3, 50, -99, 55];
$positive = array_filter($numbers, function ($number) {
	return $number > 0;
});
echo '<pre>';
print_r($positive);
  ?>

o/p:
Array
(
    [0] => 20
    [2] => 50
    [4] => 55
)


```
NOTE: There is a way to filter not only by the values. You can use ARRAY_FILTER_USE_KEY or ARRAY_FILTER_USE_BOTH as a third parameter to pass the key or both value and key to the callback function.<br>

b. Without callbacks: remove empty values i.e. 0

```
<?php
$numbers = [-1, 0, 1];
 
$not_empty = array_filter($numbers);
 
print_r($not_empty); // [0 => -1, 2 => 1]

o/p:
Array
(
    [0] => 20
    [1] => -3
    [3] => -99
    [4] => 55
)

// 0 removed

```

<b>9. array_unique()</b><br>
 You can get only unique values from an array using the array_unique() function. Notice that the function will preserve the keys of the first unique elements:<br>

```
$array = [1, 1, 1, 1, 2, 2, 2, 3, 4, 5, 5];
$uniques = array_unique($array);




Echo ‘<pre>’; 
print_r($uniques);
Array
(
    [0] => 1
    [4] => 2
    [7] => 3
    [8] => 4
    [9] => 5
)

```
<b>10. array_columns()</b><br>
 you can get a list of column values from a multi-dimensional array, like an answer from a SQL database or an import from a CSV file. Just pass an array and column name:<br>

```
$array = mysqli_fetch(----);	// this will fetch data from db
$array = [
    ['id' => 1, 'title' => 'tree'],
    ['id' => 2, 'title' => 'sun'],
    ['id' => 3, 'title' => 'cloud'],
];					// we will use static one for understanding where key is column name
 
$ids = array_column($array, 'id');
 
print_r($ids); // [1, 2, 3]

```
### With PHP7 array_column()has become more powerful it is allowed to work with objects. So working with array of models has become even more easier

```
$cinemas = Cinema::find()->all();
$cinema_ids = array_column($cinemas, 'id'); // php7 forever!

```

<b>11. array_map()</b><br>
 You can apply callback to every element of any array. You can pass function name or anonymous function and get new array based on given array.

```
$cities = ['Berlin', 'KYIV', 'Amsterdam', 'Riga'];
$aliases = array_map('strtolower', $cities);	// named function
 
print_r($aliases); // ['berlin', 'kyiv, 'amsterdam', 'riga']
 
$numbers = [1, -2, 3, -4, 5];
$squares = array_map(function($number) {		// unaninomous function
    return $number ** 2;
}, $numbers);	// 2nd parameter is array
 
print_r($squares);  // [1, 4, 9, 16, 25]

``` 
b. There is a myth that no way to pass values and keys of an array to a callback, see how it can be done

```
$model = ['id' => 7, 'name'=>'James'];
 
$callback = function($key, $value) {
    return "$key is $value";
};
 
$res = array_map($callback, array_keys($model), $model);
print_r($res);
 
// Array
// (
//     [0] => id is 7
//     [1] => name is James
// )

```
<b>12. array_walk()</b><br>
a.The above code of key value looks bit dirty, better is array_walk()
b. It doesn’t create new array but changes the new array
c. So source array is passed by reference


```
$fruits = [
    'banana' => 'yellow',
    'apple' => 'green',
    'orange' => 'orange',
];
 
array_walk($fruits, function(&$value, $key) {
    $value = "$key is $value";
});
 
print_r($fruits);
 
// Array
// (
//     [banana] => banana is yellow
//     [apple] => apple is green
//     [orange] => orange is orange

```

## Joining the Array

<b>13. array_merge()</b><br>
The best way to merge two or more arrays in PHP is to use the array_merge() function. Items of arrays will be merged together, and values with the same string keys will be overwritten with the last value:

```
$array1 = ['a' => 'a', 'b' => 'b', 'c' => 'c'];
$array2 = ['a' => 'A', 'b' => 'B', 'D' => 'D'];
 
$merge = array_merge($array1, $array2);
print_r($merge);
// Array
// (
//     [a] => A
//     [b] => B
//     [c] => c
//     [D] => D
// )

```
<b>14. array_diff()</b><br>
Removes 2nd array value from 1st array. If some extra values are there in 2nd array that is left as it is

```
$array1 = [1, 2, 3, 4];
$array2 =       [3, 4, 5, 6];
 
$diff = array_diff($array1, $array2);
print_r($diff); // [0 => 1, 1 => 2]


```
<b>15. array_intersect()</b><br>
The common value between array1 and array2 is shown

```
$array1 = [1, 2, 3, 4];
$array2 =       [3, 4, 5, 6];
 
$intersect = array_intersect($array1, $array2);
print_r($intersect);  // [2 => 3, 3 => 4]

```
## Do the Math with Array Values
<b>16. array_sum()</b><br>
Use array_sum() to get a sum of array values

```
$numbers = [1, 2, 3, 4, 5];
 
echo(array_sum($numbers)); // 15

```
<b>17. array_product()</b><br>
Use  array_product() to multiply them

```
$numbers = [1, 2, 3, 4, 5];
 
echo(array_product($numbers)); // 120

```
<b>18. array_reduce()</b><br>
create your own formula with array_reduce():<br>
Eg1. <br>

```
 
echo(array_reduce($numbers, function($carry, $item) {
    return $carry ? $carry / $item : 1;
})); // 0.0083 = 1/2/3/4/5

```
Eg2. <br>
```
<?php
function sum($carry, $item)
{
    $carry += $item;
    return $carry;
}

function product($carry, $item)
{
    $carry *= $item;
    return $carry;
}

$a = array(1, 2, 3, 4, 5);
$x = array();

var_dump(array_reduce($a, "sum")); // int(15)
var_dump(array_reduce($a, "product", 10)); // int(1200), because: 10*1*2*3*4*5
var_dump(array_reduce($x, "sum", "No data to reduce")); // string(17) "No data to reduce"

```
<b>19. array_count_values()</b><br>
To count the values of array how much time it is repeated
```
$things = ['apple', 'apple', 'banana', 'tree', 'tree', 'tree'];
$values = array_count_values($things);
 
print_r($values);
 
// Array
// (
//     [apple] => 2
//     [banana] => 1
//     [tree] => 3
// )

```

## Generating Arrays

<b>20. array_fill()</b><br>
generate an array with given size array_fill() is used
Eg
```
$bind = array_fill(0, 5, '?');	// 3rd parameter is common to all
print_r($bind); // ['?', '?', '?', '?', '?']

$bind = array_fill(0, 5, 1);	// 3rd parameter is common to all
print_r($bind); // [1, 1, 1, 1, 1]

```
<b>21. range()</b><br>
To generate an array with range of keys and values like day hours or letters, use range()
```
$letters = range('a', 'z');
print_r($letters); // ['a', 'b', ..., 'z']
 
$hours = range(0, 23);
print_r($hours); // [0, 1, 2, ..., 23]

```



<b>22. array_slice()</b><br>
To get part of an array we use array_slice(), like get first 3 element
```
$numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
$top = array_slice($numbers, 0, 3);	1st para – array, 2nd para – starting index, 3rd para – till which index
print_r($top); // [1, 2, 3]

```
<b>23. sort(), rsort(), asort(), ksort(), arsort(), krsort();</b><br>It is good to remember that every sorting function in PHP works with arrays by a reference and returns true on success or false on failure. There's a basic sorting function called sort(), and it sorts values in ascending order without preserving keys. The sorting function can be prepended by the following letters:<br>
•	sort() - sort arrays in ascending order<br>
•	rsort() - sort arrays in descending order<br>
•	asort() - sort associative arrays in ascending order, according to the value<br>
•	ksort() - sort associative arrays in ascending order, according to the key<br>
•	arsort() - sort associative arrays in descending order, according to the value<br>
•	krsort() - sort associative arrays in descending order, according to the key<br>

## Combining Array Functions Like a Boss
a.  The real magic begins when you start to combine array functions. Here is how you can trim and remove empty values in just a single line of code with array_filter() and array_map()

```
$values = ['say  ', '  bye', ' ', ' to', ' spaces ', '   '];
 
$words = array_filter(array_map('trim', $values));
print_r($words); // ['say', 'bye', 'to', 'spaces']

```
b.  To create an id to a title map from an array of models, we can use a combination of array_combine() and array_column():

```
$models = [$model1, $model2, $model3];
 
$id_to_title = array_combine(
    array_column($models, 'id'),
    array_column($models, 'title')
);

```

c.  To get the top three values of an array, we can use array_count_values(), arsort(), and array_slice():

```$letters = ['a', 'a', 'a', 'a', 'b', 'b', 'c', 'd', 'd', 'd', 'd', 'd'];
 
$values = array_count_values($letters); // get key to count array
arsort($values); // sort descending preserving key
$top = array_slice($values, 0, 3); // get top 3
 
print_r($top);
// Array
// (
//     [d] => 5
//     [a] => 4
//     [b] => 2
// )

```
d.  It is easy to use array_sum() and array_map() to calculate the sum of order in a few rows:

```
$order = [
    ['product_id' => 1, 'price' => 99, 'count' => 1],
    ['product_id' => 2, 'price' => 50, 'count' => 2],
    ['product_id' => 2, 'price' => 17, 'count' => 3],
];
 
$sum = array_sum(array_map(function($product_row) {
    return $product_row['price'] * $product_row['count'];
}, $order));
 
print_r($sum); // 250
```
