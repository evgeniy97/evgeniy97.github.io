## Utility or additional funtional

We just provide some basic metrics and base interface to add new metric now, but if you nee some more specify functionality ypu are wlcome to addres ypur suggeest to us.

# Comparison function

We provie base class model:

```python
class baseSravnyator:
    def __init__(self, function) -> None:
        self.function = function
        
    ## @staticmethod
    def __call__(self, *arg) -> tp.Union[int, float, list]:
        return self.function(*arg)
```
You can use this as:
```python
def f(a,b):
    return (a+b)/2

def g(l):
    return sum(l) 

sr_f = baseSravnyator(f)
sr_g = baseSravnyator(g)

sr_f(2,3) # -> 2.5
sr_g([1,2,3]) # -> 6
```
Or you can use pre-implemented MSE,MAE or KL functions:

```python
mse = MSESravnyator()
mse([1,2,3], [2,3,1]) # -> 2.0

mae = MAESravnyator()
mae([1,2,3], [2,3,1]) # -> 1.33333

kl = KLSravnyator()

values1 = [1.346112,1.337432,1.246655]
values2 = [1.033836,1.082015,1.117323]

kl(values1, values2) # -> 0.7752796240788413
```
