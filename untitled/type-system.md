# Type system



### Type name resolution

1. Order of search to resolve a type name:
2. Current function
3. Closure
4. Module level
5. At any level, if there are multiple candidates there will be a compiler error.
6. Two named types are never equal. 
7. Two types T1 and T2 are identical/assignable/exchangeable if they have the same structure \(e.g. `int|string` vs `int|string`\).

