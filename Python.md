#Weird-Python


#Gaussian-Rounding 

```
>>>round(5.5)
6
>>>round(6.5)
6
```
This seems really weird, but it is actually because the ```round``` function in Python is doing #Gaussian-Rounding . This means that, when rounding numbers of the form x.5, it will round to the nearest even number. This is a way to avoid bias--if we were to always round up, there would be an upwards bias.



