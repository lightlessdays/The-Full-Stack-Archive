---
title: "Reading JSON and parsing dumps"
datePublished: Sat Sep 02 2023 19:28:54 GMT+0000 (Coordinated Universal Time)
cuid: clm2f3849000209jvgswhgakw
slug: reading-json-and-parsing-dumps
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693682905849/696f81e7-0d84-4a4b-b86d-c86fad3e745d.jpeg
tags: django, rest-api

---

Today, we are going to learn how to work with JSON files in Python. Please note that I am assuming that you have a general understanding of JSON files and Python dictionaries.

![image-100](https://www.freecodecamp.org/news/content/images/2020/10/image-100.png align="left")

When we work with JSON files in Python, we can't just read them and use the data in our program directly. This is because the entire file would be represented as a single string and we would not be able to access the key-value pairs individually.

Unless... We use the key-value pairs of the JSON file to create a Python dictionary that we can use in our program to read the data, use it, and modify it (if needed).

This is the main connection between JSON and Python Dictionaries. JSON is the string representation of the data and dictionaries are the actual data structures in memory that are created when the program runs.

Luckily for us, Python comes with a built-in module called `json`. It is installed automatically when you install Python and it includes functions to help you work with JSON files and strings.

To use `json` in our program, we just need to write an import statement at the top of the file.

```python
import json
```

With this line, you will have access to the functions defined in the module. We will use several of them in the examples. If you write this import statement, you will need to use this syntax to call a function defined in the `json` module:

```python
json.function(arguments)
```

### 🔃 Deserialization / Loading

Let's take a multi-line Python string. As we already know that they are enclosed in triple quotes in Python.

```python
data_JSON =  """
{
	"size": "Medium",
	"price": 15.67,
	"toppings": ["Mushrooms", "Extra Cheese", "Pepperoni", "Basil"],
	"client": {
		"name": "Jane Doe",
		"phone": "455-344-234",
		"email": "janedoe@email.com"
	}
}
"""
```

We will use the string with JSON format to create a Python dictionary that we can access, work with, and modify. To do this, we will use the `loads()` function of the `json` module, passing the string as the argument. This is the syntax:

```python
json.loads(JSON_String)
```

So our code would be something like:

```python
data_dict = json.loads(data_JSON)
```

`json.loads(data_JSON)` creates a new dictionary with the key-value pairs of the JSON string and it returns this new dictionary.

If we print this dictionary, we see this output:

```python
{'size': 'Medium', 'price': 15.67, 'toppings': ['Mushrooms', 'Extra Cheese', 'Pepperoni', 'Basil'], 'client': {'name': 'Jane Doe', 'phone': '455-344-234', 'email': 'janedoe@email.com'}}
```

Now let's see what happens when we try to access the values of the key-value pairs with the same syntax that we would use to access the values of a regular Python dictionary:

```python
print(data_dict["size"])
print(data_dict["price"])
print(data_dict["toppings"])
print(data_dict["client"])
```

The output would be:

```python
Medium
15.67
['Mushrooms', 'Extra Cheese', 'Pepperoni', 'Basil']
{'name': 'Jane Doe', 'phone': '455-344-234', 'email': 'janedoe@email.com'}
```

When you use `loads()` to create a Python dictionary from a JSON string, you will notice that some values will be converted into their corresponding Python values and data types. Well... according to the official documentation, here is how the conversion takes place:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693680594574/6a71922b-3da0-41ea-8669-24d74822d2bd.png align="center")

### 🥟 Serialization / Dumping

But sometimes we might need to do exactly the opposite, creating a string with JSON format from an object (for example, a dictionary) to print it, display it, store it, or work with it as a string.

To do that, we can use the `dumps` function of the `json` module, passing the object as argument:

```python
json.dumps(JSON_object)
```

This is an example where we convert the Python dictionary `client` into a string with JSON format and store it in a variable:

```python
# Python Dictionary
client = {
    "name": "Nora",
    "age": 56,
    "id": "45355",
    "eye_color": "green",
    "wears_glasses": False
}

# Get a JSON formatted string
client_JSON = json.dumps(client)
```

`json.dumps(client)` creates and returns a string with all the key-value pairs of the dictionary in JSON format.

The output would look like this:

```json
{"name": "Nora", "age": 56, "id": "45355", "eye_color": "green", "wears_glasses": false}
```

A process of type conversion occurs as well when we convert a dictionary into a JSON string. So here is the table from the official documentation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693680908591/87b17fa7-9482-467b-a6e2-cd49042b30e2.png align="center")

We can improve the readability of the JSON string by adding **indentation**.

To do this automatically, we just need to pass a second argument to specify the number of spaces that we want to use to indent the JSON string:

```python
json.dumps(JSON_object, indent = number_Of_Spaces)
```

Now, if we call `dumps` with this second argument:

```python
client_JSON = json.dumps(client, indent=4)
```

The result of printing `client_JSON` is:

```python
{
    "name": "Nora",
    "age": 56,
    "id": "45355",
    "eye_color": "green",
    "wears_glasses": false
}
```

Now our string is nicely formatted.

Now we can also do stuff like sorting keys in ascending order. For that, we need to use an argument called `sort_keys`.

```python
json.dumps(<0bj>, indent=4, sort_keys=True)
```

Here, the output would be:

```json
{
    "age": 56,
    "eye_color": "green",
    "id": "45355",
    "name": "Nora",
    "wears_glasses": false
}
```

### 👁️ Reading from a .JSON File

Now that we are here, let us talk about how to read from and write to a JSON file in Python.

Let's say that we created an `orders.json` file with this data that represents two orders in a pizza shop:

```json
{
	"orders": [ 
		{
			"size": "medium",
			"price": 15.67,
			"toppings": ["mushrooms", "pepperoni", "basil"],
			"extra_cheese": false,
			"delivery": true,
			"client": {
				"name": "Jane Doe",
				"phone": null,
				"email": "janedoe@email.com"
			}
		},
		{
			"size": "small",
			"price": 6.54,
			"toppings": null,
			"extra_cheese": true,
			"delivery": false,
			"client": {
				"name": "Foo Jones",
				"phone": "556-342-452",
				"email": null
			}
		}
	]
}
```

Here is a very interesting thing to note here. The value of the main key `"orders"` is an array of JSON objects (this array will be represented as list in Python). Each JSON object holds the data of a pizza order.

If we want to read this file in Python, we just need to use a `with` statement:

```python
with open("orders.json") as file:
     data = json.load(file)
```

Here, `open("orders.json")` opens the orders.json file in read mode. `file` is our file object where data from orders.json is stored. `json.load(file)` reads the object and creates a dictionary from it.

Notice that we are using `load()` instead of `loads()`. Well... the difference between the two of them is very simple. `load()` create a Python Object from a JSON file. It takes JSON file object as an argument. `load()` create a Python Object from a String. It takes String as an argument.

The `s` in `loads()` stands for string.

### ✍️ Writing to a JSON File

Now, let us talk about writing to a JSON file. Just like `load()` and `loads()` we will be using `dump()` and `dumps()` here. We will be using `dump()` if we want to write to a file and `dumps()` if we want to write to a String. The `s` in `dumps()` stands for string.

But first we will make one small change to our `with` statement:

```python
with open("orders.json",'w') as file:
```

The only change is that you need to open the file in `'w'` (write) mode to be able to modify the file. If the file doesn't exist already in the current working directory (folder), it will be created automatically. By using the `'w'` mode, we will be replacing the entire content of the file if it already exists.

Let's say that the pizza shop wants to remove the clients' data from the JSON file and create a new JSON file called `orders_new.json` with this new version. Let us write the code for that.

```python
# Open the orders.json file
with open("orders.json") as file:
    # Load its content and make a new dictionary
    data = json.load(file)

    # Delete the "client" key-value pair from each order
    for order in data["orders"]:
        del order["client"]

# Open (or create) an orders_new.json file 
# and store the new version of the data.
with open("orders_new.json", 'w') as file:
    json.dump(data, file, indent=4)
```

Here's the output of this code:

```json
{
    "orders": [
        {
            "size": "medium",
            "price": 15.67,
            "toppings": [
                "mushrooms",
                "pepperoni",
                "basil"
            ],
            "extra_cheese": false,
            "delivery": true
        },
        {
            "size": "small",
            "price": 6.54,
            "toppings": null,
            "extra_cheese": true,
            "delivery": false
        }
    ]
}
```

This was all - thanks for reading. ❣️