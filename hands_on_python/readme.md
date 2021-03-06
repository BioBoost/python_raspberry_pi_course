# Hands on Python

In the following tutorials we will get our hands dirty and dive into some Python coding.

* [Prime Numbers](../hands_on_python/prime_numbers.md)
* [An LED class](../hands_on_python/led_class.md)
* [Solutions](../hands_on_python/solutions.md)

On the Raspberry Pi stations provided for the workshop you can use the Geany editor (found under `Start => Programming => Geany`). By selecting `File => New` you can create a new python script. Make sure to save it with a `.py` extension before starting. This way Geany will know we are writing python code.

One thing that needs to be done is to change the default python version to version 3. In Geany you can do this by changing the 'Build commands'. In the menu, go to `Build` and click on `Set build commands`. Change the `python` value to `python3` (just add a `3`) for the `Compile` and `Execute` actions like in the screenshot below.

![Make python3 the default python version](img/geany-python3-default.jpg)

If you wish you can start by creating a "Hello World" application using the code below.

```python
print("Hello World")
```

Save the script as `hello.py`. Next press `F5` or select `Build => Execute` to run the script. You should get a window with the text "Hello World" as shown in the following screenshot.

![Hello World in Python with Geany](img/hello_world.png)

Create new scripts for each tutorial. If you wish you can later email them to yourself.
