Created: 2024-09-18 20:36
## Family Tree:
1. Computer
2. Database Administration
3. [[Data Analytics]]
-- -
A **dimension** provides context to a metric. When we use a dimension, we are assigning a qualitative value to our metric, such as "user type," "source," "medium," "country," "city," "customer name," etc. Dimensions can be used to break down another field or to measure data in distinct groups. They also help define the level of detail at which an aggregation should be performed.
For example, we can use the **"sum of sales"** as a measure and then use **"region"** as a dimension field to divide the "sum of sales" by region.
## Characteristics
- They provide **context** to our data.
- Allow for **segmentation, classification,** and **filtering** of information.
- They are **qualitative** in nature.
## Measures
Measures are fields that can be aggregated in some way, such as through a sum or an average. Think of them as data that can be collected, counted, or combined to return a single value.

Dimensions help give context to our data, and a good way to guide their use is by thinking of the **5 W's**:
- **Why:** Why did it happen?
- **When:** When did it happen?
- **What:** What happened?
- **Where:** Where did it happen?
- **Who:** Who was involved?