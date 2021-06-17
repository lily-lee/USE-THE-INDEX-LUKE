# USE-THE-INDEX-LUKE 中文翻译

原文 https://use-the-index-luke.com

<details><summary>原文目录链接</summary>

## Table of Contents

1. *[Preface](https://use-the-index-luke.com/sql/preface)* — Why is indexing a development task?
2. *[Anatomy of an Index](https://use-the-index-luke.com/sql/anatomy)* — What does an index look like?
    1. *[The Leaf Nodes](https://use-the-index-luke.com/sql/anatomy/the-leaf-nodes)* — A doubly linked list
    2. *[The B-Tree](https://use-the-index-luke.com/sql/anatomy/the-tree)* — It’s a balanced tree
    3. *[Slow Indexes, Part I](https://use-the-index-luke.com/sql/anatomy/slow-indexes)* — Two ingredients make the index slow
3. *[The Where Clause](https://use-the-index-luke.com/sql/where-clause)* — Indexing to improve search performance
    1. *[The Equals Operator](https://use-the-index-luke.com/sql/where-clause/the-equals-operator)* — Exact key lookup
        1. *[Primary Keys](https://use-the-index-luke.com/sql/where-clause/the-equals-operator/primary-keys)* — Verifying index usage
        2. *[Concatenated Keys](https://use-the-index-luke.com/sql/where-clause/the-equals-operator/concatenated-keys)* — Multi-column indexes
        3. *[Slow Indexes, Part II](https://use-the-index-luke.com/sql/where-clause/the-equals-operator/slow-indexes-part-ii)* — The first ingredient, revisited
    2. *[Functions](https://use-the-index-luke.com/sql/where-clause/functions)* — Using functions in the `where` clause
        1. *[Case-Insensitive Search](https://use-the-index-luke.com/sql/where-clause/functions/case-insensitive-search)* — `UPPER` and `LOWER`
        2. *[User-Defined Functions](https://use-the-index-luke.com/sql/where-clause/functions/user-defined-functions)* — Limitations of function-based indexes
        3. *[Over-Indexing](https://use-the-index-luke.com/sql/where-clause/functions/over-indexing)* — Avoid redundancy
    3. *[Bind Variables](https://use-the-index-luke.com/sql/where-clause/bind-parameters)* — For security and performance
    4. *[Searching for Ranges](https://use-the-index-luke.com/sql/where-clause/searching-for-ranges)* — Beyond equality
        1. *[Greater, Less and `BETWEEN`](https://use-the-index-luke.com/sql/where-clause/searching-for-ranges/greater-less-between-tuning-sql-access-filter-predicates)* — The column order revisited
        2. *[Indexing SQL `LIKE` Filters](https://use-the-index-luke.com/sql/where-clause/searching-for-ranges/like-performance-tuning)* — `LIKE` is not for full-text search
        3. *[Index Combine](https://use-the-index-luke.com/sql/where-clause/searching-for-ranges/index-merge-performance)* — Why not using one index for every column?
    5. *[Partial Indexes](https://use-the-index-luke.com/sql/where-clause/partial-and-filtered-indexes)* — Indexing selected rows
    6. *[`NULL` in the Oracle Database](https://use-the-index-luke.com/sql/where-clause/null)* — An important curiosity
        1. *[`NULL` in Indexes](https://use-the-index-luke.com/sql/where-clause/null/index)* — Every index is a partial index
        2. *[`NOT NULL` Constraints](https://use-the-index-luke.com/sql/where-clause/null/not-null-constraint)* — affect index usage
        3. *[Emulating Partial Indexes](https://use-the-index-luke.com/sql/where-clause/null/partial-index)* — using function-based indexing
    7. *[Obfuscated Conditions](https://use-the-index-luke.com/sql/where-clause/obfuscation)* — Common anti-patterns
        1. *[Dates](https://use-the-index-luke.com/sql/where-clause/obfuscation/dates)* — Pay special attention to `DATE` types
        2. *[Numeric Strings](https://use-the-index-luke.com/sql/where-clause/obfuscation/numeric-strings)* — Don’t mix types
        3. *[Combining Columns](https://use-the-index-luke.com/sql/where-clause/obfuscation/concatenation)* — use redundant `where` clauses
        4. *[Smart Logic](https://use-the-index-luke.com/sql/where-clause/obfuscation/smart-logic)* — The smartest way to make SQL slow
        5. *[Math](https://use-the-index-luke.com/sql/where-clause/obfuscation/math)* — Databases don’t solve equations
4. *[Testing and Scalability](https://use-the-index-luke.com/sql/testing-scalability)* — About hardware
    1. *[Data Volume](https://use-the-index-luke.com/sql/testing-scalability/data-volume)* — Sloppy indexing bites back
    2. *[System Load](https://use-the-index-luke.com/sql/testing-scalability/system-load)* — Production load affects response time
    3. *[Response Time and Throughput](https://use-the-index-luke.com/sql/testing-scalability/response-time-throughput-scaling-horizontal)* — Horizontal scalability
5. *[The Join Operation](https://use-the-index-luke.com/sql/join)* — Not slow, if done right
    1. *[Nested Loops](https://use-the-index-luke.com/sql/join/nested-loops-join-n1-problem)* — About the N+1 selects problem in ORM
    2. *[Hash Join](https://use-the-index-luke.com/sql/join/hash-join-partial-objects)* — Requires an entirely different indexing approach
    3. *[Sort-Merge Join](https://use-the-index-luke.com/sql/join/sort-merge-join)* ‌— Like a zipper on two sorted sets
6. *[Clustering Data](https://use-the-index-luke.com/sql/clustering)* — To reduce IO
    1. *[Index Filter Predicates Intentionally Used](https://use-the-index-luke.com/sql/clustering/index-filter-predicates)* — to tune `LIKE`
    2. *[Index-Only Scan](https://use-the-index-luke.com/sql/clustering/index-only-scan-covering-index)* — Avoiding table access
    3. *[Index-Organized Table](https://use-the-index-luke.com/sql/clustering/index-organized-clustered-index)* — Clustered indexes without tables
7. *[Sorting and Grouping](https://use-the-index-luke.com/sql/sorting-grouping)* — Pipelined `order by`: the third power
    1. *[Indexed Order By](https://use-the-index-luke.com/sql/sorting-grouping/indexed-order-by)* — `where` clause interactions
    2. *[`ASC`/`DESC` and `NULL FIRST`/`LAST`](https://use-the-index-luke.com/sql/sorting-grouping/order-by-asc-desc-nulls-last)* — changing index order
    3. *[Indexed Group By](https://use-the-index-luke.com/sql/sorting-grouping/indexed-group-by)* — Pipelining `group by`
8. *[Partial Results](https://use-the-index-luke.com/sql/partial-results)* — Paging efficiently
    1. *[Selecting Top-N Rows](https://use-the-index-luke.com/sql/partial-results/top-n-queries)* — if you need the first few rows only
    2. *[Fetching The Next Page](https://use-the-index-luke.com/sql/partial-results/fetch-next-page)* — The offset and seek methods compared
    3. *[Window-Functions](https://use-the-index-luke.com/sql/partial-results/window-functions)* — Pagination using analytic queries
9. *[Insert, Delete and Update](https://use-the-index-luke.com/sql/dml)* — Indexing impacts on DML statements
    1. *[Insert](https://use-the-index-luke.com/sql/dml/insert)* — cannot take direct benefit from indexes
    2. *[Delete](https://use-the-index-luke.com/sql/dml/delete)* — uses indexes for the `where` clause
    3. *[Update](https://use-the-index-luke.com/sql/dml/update)* — does not affect all indexes of the table

</details>
