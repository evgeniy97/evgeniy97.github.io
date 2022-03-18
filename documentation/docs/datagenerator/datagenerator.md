## Data generator

We consider that both machine learning and popuation genomics are data-first fields of scince. So we stress out how we generate data (as far as we cannot use real data).

As core we use msprime generator [1] and provide some wrapper on it.


## Easy start

The easiet way to generaate some data is following:
```python

from ??? import *

# generate demographics evevents structure 
demographics_evevents = generate_demographic_events_complex(12000, random_seed=47)

DG = DataGenerator(demographic_events=demographics_evevents)

for mutations, d_times, prior_dist in DG:
    pass # do whatever you want

print(mutations[:100], d_times[:100], prior_dist)
>> [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1] [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] [0.25771900000000003, 0.05625199999999999, 0.019091, 0.06374333333333333, 0.19882266666666665, 0.03460433333333332, 0.03325966666666667, 0.011786333333333334, 0.016540666666666665, 0.021863999999999995, 0.017948333333333334, 0.02438633333333334, 0.010525666666666668, 0.03543433333333334, 0.010777999999999998, 0.008822333333333335, 0.052617, 0.11978399999999996, 0.005343999999999999, 0.0006770000000000001]
```
so, the output of DataGenerator is mutations (0 for not mutatation in a locus), actual discreted coaleescentee time and prior colescent time distribution. 

## Demographic history


As we show adove, you can generate random  demographics evevents by using generate_demographic_events_complex function:

```python
generate_demographic_events_complex(int: population, int: random_seed) -> msprime.Demography
population: int - is the initial population size

output:
    msprime.Demography object
```
or you can initialize msprime.Demography object from two list:
```python

demographics_evevents(List[int]: time, List[int]: population_sizes, int: random_seed) -> msprime.Demography


demographics_evevents = generate_demography_from_list(
    [1_000, 2_000, 3_000, 4_000, 5_000, 6_000 ],
    [100, 1000, 100, 1_000, 500, 1_000]
)

```

If you are familiar with msprime you can create demographics_evevents as usual

some tip for visualization:
```python

debug = generate_demography_from_list(
    [1_000, 2_000, 3_000, 4_000, 5_000, 6_000 ],
    [100, 1000, 100, 1_000, 500, 1_000]
).debug()

t = np.linspace(0, 10_000, num=20)
S = debug.population_size_trajectory(t)
plt.step(t, S, label="Population")
plt.xlabel("Time ago")
plt.ylabel("Population size")
plt.legend()
```

## Generator

```python
DG = DataGenerator(demographic_events=demographics_evevents)

for mutations, d_times, prior_dist in DG:
    pass # do whatever you want

print(mutations[:100], d_times[:100], prior_dist)
>> [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1] [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] [0.25771900000000003, 0.05625199999999999, 0.019091, 0.06374333333333333, 0.19882266666666665, 0.03460433333333332, 0.03325966666666667, 0.011786333333333334, 0.016540666666666665, 0.021863999999999995, 0.017948333333333334, 0.02438633333333334, 0.010525666666666668, 0.03543433333333334, 0.010777999999999998, 0.008822333333333335, 0.052617, 0.11978399999999996, 0.005343999999999999, 0.0006770000000000001]
```

```python
class DataGenerator(self,
                 recombination_rate: float = RHO_HUMAN,
                 mutation_rate: float = MU_HUMAN,
                 demographic_events: list = None,
                 population: int = None,
                 number_intervals: int = N,
                 splitter=simple_split,
                 num_replicates: int = 1,
                 lengt: int = L_HUMAN,
                 model: str = "hudson",
                 random_seed: int = 42,
                 mutation_random_seed: int = 42,
                 sample_size: int = 1,
                 )
```

------ 
[1] Jerome Kelleher, Alison M Etheridge and Gilean McVean (2016), Efficient Coalescent Simulation and Genealogical Analysis for Large Sample Sizes, PLOS Comput Biol 12(5): e1004842. doi: 10.1371/journal.pcbi.1004842


