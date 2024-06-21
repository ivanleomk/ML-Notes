Function Calling Models
- Used to only return a function, it will always return a function
- FC -> A LLM that returns a valid string
- Tool -> The actual func called

Interesting docstring + .inspect usage to generate automatic definitions

Variations of function calling
- Parallel Calls -> Instructor Iterable (Eg. can you help me to create two clowns. Clown 1 has xx and Clown 2 has yy)
- Multiple Functions -> Giving it a clown and a draw tie func and getting it to choose 1
- Multiple Parllel Func Call -> instructor Iterable with Union Type
- Nested APIs -> Just seems like a simple bunch of smaller queries? Eg. Combine x,y and z. Could be solved with a large main type and 5 smaller subtypes lol

Using a python dataclass...directly inside the prompt itself