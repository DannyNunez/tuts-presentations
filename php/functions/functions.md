### Basic Syntax

To create a function the keyword *function* is used and than followed by an *identifier* "the function name" , a pair of parenthese and curly braces. 

```
function name(){
}
```

PHP function names are not case-sensitive. 

The *identifiers* in PHP must consist only letters(a-z), numbers and the underscore character, and must not start with a number. 

To make your function do something simple place the code to be executed between the braces, and than call it. 

```
function hello(){
    echo "Hello World!"
}
hello(); // "Hello World!"
```

###Returning Values

All functions in PHP return a value-even if you do not explicitly cause them to. The concept of "Void" Functions does not really apply to PHP. You can specify the return value of your function by using the return keyword. 

Even if you do not return a value, 

```
function name(){
    return "HELLO!";
}
```




### is_scalar()

Scalar variables are those containing an integer, float, string or boolean. Types array, object and resource are not scalar.