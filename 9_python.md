# Python for Cybersecurity



**01. What is the correct way to write a Python script with proper syntax?**

A well-written Python script relies on correct indentation (usually 4 spaces) to define code blocks instead of curly braces. It generally begins with a "shebang" line on UNIX-based OS (Operating System) environments (e.g., `#!/usr/bin/env python3`), followed by `import` statements, variable declarations, and function definitions. The main execution code is usually placed under an `if __name__ == "__main__":` block to prevent it from running automatically if the script is imported as a module into another file.

**02. What are variables, data types, and operators used for in Python?**

Variables store data under a name so you can reference and reuse it (e.g. `x = 5`). Data types describe the kind of value stored, such as `int` (integer), `float` (floating-point number), `str` (string), `bool` (boolean), `list` (list), `dict` (dictionary), and `tuple` (tuple). Operators perform actions on values: arithmetic (`+`, `-`, `*`, `/`), comparison (`==`, `!=`, `<`, `>`), logical (`and`, `or`, `not`), and assignment (`=`, `+=`).

**03. What conditions would you use to implement `if`, `elif`, and `else` statements?**

You use conditions that evaluate to a boolean (`True` or `False`). if tests the first condition; `elif` (else-if) tests an alternative condition when the previous ones were false; `else` runs when none of the conditions matched. Example:
```python
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
else:
    grade = "F"
```

**04. What is the difference between a `for` loop and a `while` loop, and when do you use each?**

A `for` loop iterates over a known sequence (like a `list`, `tuple`, or `string`); you use it when you know the exact number of times you need to iterate or when you want to process every item in a collection. A `while` loop continues to execute as long as a specific condition remains true; you use it when the number of iterations is unknown in advance and depends on a dynamic condition.
> **My Notes**:
> * `for` and `while` loops can use `break` to exit early and `continue` to skip the current iteration and move to the next one.
> * `for` and `while` loops can use `else` blocks that execute if the loop completes without hitting a `break` statement.
> * `for` and `while` loops are basically equivalent in functionality, a `for` loop can be rewritten as a `while` loop and vice versa. (e.g., in 42 school C programming we were constrained to use only `while` loops and we got used to it :-))
> * I would use one or the other depending which one is more readable and makes more sense in the context of the problem. For example if I have to wait for user input I would use a `while` loop, but to manipulate every item in a list I would use a `for` loop, etc.

**05. What is a function in Python, and how do you define and call it with parameters and return values?**

A function is a reusable block of code designed to perform a specific task. You define it using the `def` keyword, followed by the function name and parameters in parentheses (e.g., `def add_numbers(a, b):`). Inside the function, you use the `return` keyword to send the calculated value back to the caller. You call it by referencing its name and passing the required arguments (e.g., `result = add_numbers(3, 4)`).

```python
def add_numbers(a, b):     # and b are parameters
	return a + b           # returns a value

result = add_numbers(3, 4) # call with arguments 3 and 4
```

**06. What is the `socket` module used for, and how do you import and use it in a script?**

The `socket` module provides low-level networking access, letting your program create network connections, send and receive data, and perform tasks like resolving hostnames or checking ports. You import it with `import socket` and then call its functions:

```python
import socket
ip = socket.gethostbyname('example.com')  # Resolves hostname to IP
print(ip)
```

```python
import socket

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:  # Create a TCP/IP socket
	# AF_INET specifies IPv4, SOCK_STREAM specifies TCP
	result = s.connect_ex(('example.com', 80))  # Check if port 80 is open
	if result == 0:
		print("Port is open")
	else:
		print("Port is closed")
```

**07. What are Python's built-in functions like `input()`, `print()`, `len()`, and `open()` used for?**

*   `input()`: Pauses the script to read a line of text entered by the user via the keyboard.
*   `print()`: Outputs text, variables, or data to the console or standard output.
*   `len()`: Returns the length (the number of items) of an object, such as a string, list, or dictionary.
*   `open()`: Opens a file on your system and returns a file object so you can perform I/O (Input/Output) operations like reading or writing.

**08. What do string methods such as `.strip()`, `.split()`, and `.format()` allow you to do?**

*   `.strip()`: Removes leading and trailing whitespace (or specific target characters) from a string.
*   `.split()`: Breaks a string apart into a list of smaller strings based on a specific delimiter (a space by default).
*   `.format()`: inserts values into a string using placeholder braces `{}`

```python
"  hi  ".strip()              # "hi"
"a,b,c".split(",")            # ["a", "b", "c"]
"Hello {}".format("World")    # "Hello World"
```

**09. What operations can you perform on Python lists?**

Lists support:
* adding items: `.append()`, .`insert()`, `.extend()`
* removing items: `.remove()`, .`pop()`, `del`
* accessing items by index or slice: `my_list[0]`, `my_list[1:3]`
* sorting: `.sort()`, `sorted()`
* reversing: `.reverse()`
* searching: `.index()`, `in`
* counting: `.count()`
* finding length: `len()`

Lists are mutable, so they can be changed after creation.

**10. What command do you use to install Python packages using `pip`?**

You use `pip install package_name`, where `pip` is the Package Installer for Python. For example, `pip install requests`. To install a specific version, use `pip install requests==2.31.0`.

**11. What steps are needed to import and use external modules such as `dnspython`, `requests`, or `beautifulsoup4`?**

First install the package with `pip` (Package Installer for Python), for example `pip install requests beautifulsoup4 dnspython`. Then import it in your script using the correct import name (which sometimes differs from the install name): `import requests`, `from bs4 import BeautifulSoup`, and `import dns.resolver`. After importing, you call the module's functions and classes as documented, e.g., `requests.get()`.

**12. What should you look for when reading and understanding Python library documentation?**

Look for:
- the installation instructions
- a quickstart or getting-started example
- the list of available functions/classes and their parameters
- expected return values, required versus optional arguments
- error/exception behavior
- code examples.

It also helps to note version requirements and any dependencies.

**13. What is the proper way to use third-party APIs effectively in a Python script?**

Read the API (Application Programming Interface) documentation to understand its endpoints, required parameters, and authentication. Using a library like `requests`, supply any needed API keys or tokens securely (not hard-coded in shared code), send requests to the correct endpoints, check the response status code, parse the returned data (often JSON — JavaScript Object Notation), and handle errors and rate limits gracefully.

**14. What methods can you use to read text files using `open()` and context managers?**

Open the file with a context manager (`with` statement), which automatically closes the file afterward. Then use `.read()` to read the whole file as one string, `.readline()` to read one line, or `.readlines()` to read all lines into a list. You can also iterate directly over the file object line by line.

```python
with open('file.txt', 'r') as f:
	content = f.read()          # Read entire file
	f.seek(0)                   # Move cursor back to the start
	first_line = f.readline()   # Read one line
	remaining_lines = f.readlines()   # Read all lines but first line
```

**15. What are the correct techniques to write data to files in Python?**

You should open the file using a context manager in write mode (`'w'`) or append mode (`'a'`). Then, you use the `.write(string)` method to write a single block of text or `.writelines(list_of_strings)` to write an iterable sequence of strings to the file.

```python
with open('output.txt', 'w') as f:
	f.write("Hello, World!\n")  # Write a single line
	f.writelines(["Line 1\n", "Line 2\n"])  # Write multiple lines
```

**16. What is the right way to parse file content line by line?**

Open the file with a context manager and iterate over the file object directly, which yields one line at a time and is memory-efficient. Use `.strip()` to remove the trailing newline from each line.

```python
with open('file.txt', 'r') as f:
    for line in f:
        print(line.strip())
```

**17. What are the file modes (`'r'`, `'w'`, `'a'`), and what is each one used for?**

*   `'r'` (Read): Used for reading data from an existing file. It will throw an error if the file does not exist.
*   `'w'` (Write): Used for writing data. It creates a new file if one doesn't exist, or completely overwrites (truncates) an existing file.
*   `'a'` (Append): Used to add new data to the end of a file without deleting the existing content. It creates a new file if it doesn't exist.

**18. How do you resolve a domain to an IP address in Python?**

You import the built-in `socket` module and use its functions, most commonly passing the domain name as a string to the `socket.gethostbyname()` function, which will return the IP (Internet Protocol) address.

```python
import socket
ip = socket.gethostbyname("example.com")
print(ip)
```

**19. What is `socket.gethostbyname()` used for?**

It is used to translate a human-readable hostname (like `example.com`) into its corresponding IPv4 (Internet Protocol version 4) address format (like `172.66.147.243`). This is a basic form of DNS (Domain Name System) resolution.

**20. What library do you use for advanced DNS queries?**

For advanced DNS (Domain Name System) queries—such as looking up MX (Mail Exchange), TXT (Text), CNAME (Canonical Name), NS (Name Server), or AAAA (IPv6) records—you typically use the third-party `dnspython` library (imported as `dns` or `dns.resolver`).

**21. How do you make an HTTP GET request in Python?**

Using the `requests` library, you use the `get` method and pass the target URL (Uniform Resource Locator) as a parameter. For example: `response = requests.get('http://example.com')`.

**22. What library do you use for HTTP requests in Python?**

While Python has a built-in `urllib` module, the third-party `requests` library is the overwhelming standard because it is far simpler, more readable, and easier to use for making HTTP (Hypertext Transfer Protocol) requests. It provides simple methods like `.get()`, `.post()`, `.put()`, and `.delete()`.

**23. How do you access response headers in Python?**

If you are using the `requests` library, you can access the headers of an HTTP (Hypertext Transfer Protocol) response by looking at the `.headers` attribute of the response object (e.g., `response.headers`). This returns a dictionary-like object where you can look up specific headers (e.g., `response.headers['Content-Type']`).

```python
import requests
response = requests.get('http://example.com')
print(response.headers['Content-Type'])  # Outputs the Content-Type header
```

**24. How do you check if a port is open in Python?**

You import the `socket` module, instantiate a socket object, and use the `.connect_ex((ip_address, port_number))` method. If the method returns `0`, it means the port is open and accepting connections.

```python
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) # Create a TCP/IP socket
result = s.connect_ex(("example.com", 80))
if result == 0:
    print("Port is open")
s.close()
```

**25. What does `socket.connect_ex()` return for an open port?**

It returns the integer `0` to indicate a successful connection (meaning the port is open). If the port is closed or blocked, it returns a positive integer representing the underlying C-level network error code (like `111` for "Connection refused").
> Note: the `.connect()` is similar but raises an exception on failure instead of returning an error code.

**26. What library is used to parse HTML in Python?**

The most popular third-party library for parsing HTML (HyperText Markup Language) and XML (eXtensible Markup Language) in Python is `beautifulsoup4` (imported as `bs4` and usually used via the `BeautifulSoup` class).

**27. What is `BeautifulSoup` used for?**

`BeautifulSoup` is used to navigate, search, and extract specific data from raw HTML (HyperText Markup Language) or XML (eXtensible Markup Language) code easily. It turns a complex text document into a tree of Python objects that can be easily queried (like finding all `<a>` tags or elements with a specific class). Elements can be extracted by tag, attribute, class or identifier. It let's you modify the tree or convert it back to a string for output.

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(html_content, "html.parser")
title = soup.find("title").text
```

**28. What does `.prettify()` do?**

The `.prettify()` method takes a parsed `BeautifulSoup` HTML (HyperText Markup Language) or XML (eXtensible Markup Language) document and formats it into a visually readable string, adding appropriate spacing, indentation, and line breaks to represent the nested structure of the tags.

**29. What is web scraping?**

Web scraping is the automated process of extracting specific data from web pages — for example, pulling prices, headlines, or links out of a page's HTML (Hypertext Markup Language). It typically involves fetching a page (often with `requests`) and then parsing it (often with `BeautifulSoup`) to pull out the desired information.

**30. What is web crawling?**

Web crawling is the automated process of systematically browsing and discovering web pages. A crawler (or spider) visits a page, reads it, finds hyperlinks on that page, and follows those URLs (Uniform Resource Locators) to visit other pages, effectively mapping the structure or indexing the content of a website and all other linked pages/sites.

**31. What is recursion and how is it used in web crawling?**

Recursion is a technique where a function calls itself to solve a problem by breaking it into smaller sub-problems, with a base case that stops the calls. In web crawling, a recursive function can visit a page, extract its links, then call itself on each newly found link to explore deeper — continuing until it hits a limit (like a maximum depth) or runs out of new pages. To avoid infinite loops, crawlers track already-visited URLs (Uniform Resource Locators) so the same page isn't processed twice.
