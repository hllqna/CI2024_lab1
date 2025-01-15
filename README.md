The present approach to set covering problem was created partially thanks to the discussions with Davide Monaco (*s305133*).

## Observations for the solution:
1. The least costly sets are the sets covering just 1 element (their cost is 1). Practically, to cover elements A and B, it's better to take a set covering only A and a set covering only B (the total cost = 1 + 1 = 2) rather than take a set that covers both A and B (the cost = 2^1.1 > 2).
2. Following the same logic, the sets covering fewer elements are preferrable. Two sets covering two distinctive elements each without overlapping would cost 2*(2^1.1) = 4.287, while one set covering all those 4 elements has a greater cost of 4^1.1 = 4.5948.
3. To reduce risk of paying twice for the sets covering exactly the same elements, we can first sort out the duplicates among the covering sets.

The proposed algorithm first tries to build the valid solution by taking all unique sets covering only one element and iteratively adding a randomly picked set of the smallest number of elements, until the valid solution is composed. At this point, we don't explicitly care about the cost. The idea is that by choosing this initialisation, we start with a solution which cost by a construction is kept low. In our approach we are more likely to start local search in a state close to the global optimum. Empitical observations showed, that our initialisation has a cost up to 60 times less than a random initialisation, while building takes relatively short time in all the proposed settings.
As a second step, the random mutation hill climbing is performed. At each step multiple mutations are executed, with the probability of mutation controlled by a self-adapting *temperature* parameter. Adjustment of *temperature* is done according to the 1/5 success rule, evaluated at the end of each era of hill climber.

## Results
| Instance | Universe Size | # of sets | Density | # of calls | Cost |
|----------|---------------|-----------|---------|------------|------|
| 1 | 100 | 10 | 0.2 | 10001 | 238 |
| 2 | 1000 | 100 | 0.2 | 10001 | 6080 |
| 3 | 10000 | 1000 | 0.2 | 10001 | 118044 |
| 4 | 100000 | 10000 | 0.1 | 10001 | 1928891 |
| 5 | 100000 | 10000 | 0.2 | 10001 | 2109685 |
| 6 | 100000 | 10000 | 0.3 | 10001 | 2233133 |
