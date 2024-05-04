
There are three core components of recommendation systems: The collector, ranker and server

- Collector: Know what is in the collection of things to be recommended
- Ranker : Re-order the collection provided
- Server: Take the ordered subset and ensure that the necessary data schema is satisfied and return the requested number of recommendations. 


| Method            | Collector                                   | Ranker                    | Server                               |
| ----------------- | ------------------------------------------- | ------------------------- | ------------------------------------ |
| Random Choice     | A random id is generated                    | This is a no-op           | We then return a chosen item or none |
| Most Popular Item | Get the popularity for each individual item | Rank by sorting on values | Return either a list of items or non | 

