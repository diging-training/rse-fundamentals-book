---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Code Examples

```{code-cell} ipython3
a = float(input("Please, enter a number: "))
b = (a * 1.8) + 32 

print("The result is: {0}".format(b)) 
```

```{code-cell} ipython3
celsius = float(input("Please, enter temperature in Celsius: "))
fahrenheit = (celsius * 1.8) + 32 
print("{0} Celsius is {1} Fahrenheit.".format(celsius, fahrenheit)) 
```


```{code-cell} ipython3

input = ... # retrieved or passed in from somewhere

los = []
norms = []
highs = []

for x in input:
    if x < 97:
        los.append(x)
    elif x > 99:
        highs.append(x)
    else:
        norms.append(x)  
```


```{code-cell} ipython3
normal_low = 97 # normal human body temperature lower end
normal_high = 99 # normal human body temperature higher end

temperature_measurements = ... # retrieved or passed in from somewhere

low_temperatures = []
normal_temperature = []
high_temperatures = []

for temperature in temperature_measurements:
    if temperature < normal_low:
        low_temperatures.append(temperature)
    elif temperature > normal_high:
        high_temperatures.append(temperature)
    else:
        normal_temperatures.append(temperature)  
```


```{code-cell} ipython3
normal_low = 97 # normal human body temperature lower end

temperature_measurements_1 = ... # retrieved or passed in from somewhere

normal_temperature_1 = []
high_temperatures_2 = []
normal_high = 99 # normal human body temperature higher end
low_temperatures_1 = []
low_temperatures_2 = []
normal_temperature_2 = []
high_temperatures_1 = []

for temperature in temperature_measurements:
    if temperature < normal_low:
        low_temperatures_1.append(temperature)
    elif temperature > normal_high:
        high_temperatures_1.append(temperature)
    else:
        normal_temperatures_1.append(temperature)  

temperature_measurements_2 = ... # retrieved or passed in from somewhere
for temperature in temperature_measurements_2:
    if temperature < normal_low:
        low_temperatures_2.append(temperature)
    elif temperature > normal_high:
        high_temperatures_2.append(temperature)
    else:
        normal_temperatures_2.append(temperature)  

```


```{code-cell} ipython3
NORMAL_LOW = 97 # normal human body temperature lower end
NORMAL_HIGH = 99 # normal human body temperature higher end

def sort_temperatures(measurements):
    low = []
    normal = []
    high = []

    for temperature in measurements:
        if temperature < NORMAL_LOW:
            low.append(temperature)
        elif temperature > NORMAL_HIGH:
            high.append(temperature)
        else:
            normals.append(temperature)  
    
    return low, normal, high


temperature_measurements_1 = ... # retrieved or passed in from somewhere
temperature_measurements_2 = ... # retrieved or passed in from somewhere

low_1, normal_1, high_1 = sort_temperatures(temperature_measurements_1)
low_2, normal_2, high_2 = sort_temperatures(temperature_measurements_2)

```


```{code-cell} ipython3
input = [[97, 96, 96], [99, 98,99], [96, 96, 97], [100, 99, 100]] # some array of arrays with input data
low_temps = []
low_count = 0
high_count = 0
for value in input:

    LOW_TEMP = 97
    average = 0
    if sum(value)/len(value) < LOW_TEMP:
        average = sum(value)/len(value)
        low_count += 1
    if average > 99:
        average = sum(value)/len(value)
        high_count += 1
    average = sum(value)/len(value)

    if average > 97 and average < 99:
        continue

    print("Average is " + str(average))

measurement_count = len(input)
low_percent = low_count/measurement_count*100
print("Low temperatures in {0}%.".format(low_percent))

```


```{code-cell} ipython3
from collections import Counter

measurements = [[97, 96, 96], [99, 98,99], [96, 96, 97], [100, 99, 100]] # some array of arrays with input data
LOW_TEMP = 97
HIGH_TEMP = 99

def get_average(temperatures):
    return sum(temperatures)/len(temperatures)

def count_average(average, counter):
    if average < LOW_TEMP:
        counter['low'] += 1
    if average > HIGH_TEMP:
        counter['high'] += 1

def calculate_percentage(count, total):
    return count/total*100

average_counter = Counter({'low': 0, 'high': 0})

for temperatures in measurements:
    average = get_average(temperatures)
    print("Average is " + str(average))

    if average > 97 and average < 99:
        continue

    count_average(average, average_counter)
    
measurement_count = len(measurements)

print("Low temperatures in {0}%.".format(calculate_percentage(average_counter['low'], measurement_count)))
print("High temperatures in {0}%.".format(calculate_percentage(average_counter['high'], measurement_count)))

```