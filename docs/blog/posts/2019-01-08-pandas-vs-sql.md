---
draft: false
title: "pandas vs. SQL"
date: 2019-01-08
slug: pandas-vs-sql
categories:
  - data science
tags:
  - pandas
---

As I'm starting to learn pandas, I noticed that it seems to have the 
capabilities of doing everything that SQL can do, and more. So I was curious 
about whether I would need SQL in a data science career, or if pandas could 
suffice.

A quick search turned up [this article about PostgreSQL vs. pandas](https://medium.com/carwow-product-engineering/sql-vs-pandas-how-to-balance-tasks-between-server-and-client-side-9e2f6c95677).
My takeaway is that, not surprisingly, the situation is more complex than 
simply one tool always being better than the other. Instead, SQL is best 
suited for certain tasks, and vice versa for pandas.

In particular, SQL is faster for typical database tasks, such as joins. 
Whereas pandas is better for complex operations like string manipulation or 
statistics.

While, in theory, you could do practically everything with either tool, it 
wouldn't be the most performant solution (pandas and SQL are each faster at 
certain tasks, under certain situations), nor the most desirable 
solution (e.g. SQL is a *lingua franca* and compatible with lots of 
programming languages, so pandas could be limiting in that regard).

The article, titled ["PostgreSQL vs. pandas — how to balance tasks between 
server and client side"](https://medium.com/carwow-product-engineering/sql-vs-pandas-how-to-balance-tasks-between-server-and-client-side-9e2f6c95677),
offers these ten rules of thumb for evaluating whether to use SQL or pandas 
for an analytics task:

> 1. If doing a task in SQL can cut the amount of data returned to the client 
(e.g. filtering to a smaller subset of data), then the task belongs on the 
server.
> 2. If the amount of data returned to the client remains unchanged or grows
 (e.g. adding complex calculated columns; cross-joins, etc.) by doing it in 
 SQL, the task belongs into client side code.
> 3. Test different setups on the server and client side to see which is more 
efficient. In the worst case, you’ll learn something.
> 4. Never do in code what the SQL server can do **well** for you: Data 
extraction 
(CRUD, joins and set operations) & simple data analysis.
> 5. If it’s painful or ugly, do it in client-side code: Complex data analysis 
belongs into code. Leave formatting or math for the client side. The database 
exists mainly to facilitate fast extraction of data.
> 6. Minimise SQL complexity: Split overly complex, non-performant queries. 
Two simpler queries will save the headache of maintaining one mega-query. 
Alternatively, split it into a simple query and handle the complexity in 
client-side code.
> 7. Minimise database round trips: Try to do as much as you can in one 
operation. Every semicolon is one round trip and adds another I/O operation.
> 8. Configure your database carefully e.g. for [postgres](http://pgtune.leopard.in.ua/). 
Otherwise, you default to sub-optimal algorithms which is expensive.
> 9. It’s well worth investing time in database schema optimisation.
> 10. Same goes for setting optimal foreign/sort/distribution keys and 
properly normalised tables to maintain the integrity of data.

I think the full article is a worthwhile read.