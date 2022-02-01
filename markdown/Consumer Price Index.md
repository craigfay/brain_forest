# The Consumer Price Index
In the U.S., the Bureau of Labor Statistics (BLS) produces the Consumer Price Index (CPI), which is widely used to measure the rate of inflation, and Gross Domestic Product.

Among [[Economics|economists]], there is controversy about the adequacy of the CPI calculation. The calculation has undergone revisions over the years, including a switch from a "Cost of Goods" index to a "Cost of Living" index, which some critics believe is a way for the government to deceptively report lower inflation.

## The Index Number Problem
Economists have introduced different methods for measuring inflation which are not compatible with one another.

## The Paasche Index
Developed by the German economist and statistician Herman Paasche, this very popular method of calculating CPI is given by:

$$
P_{p} = \frac
	{ \sum p_{c,t_{n}} \cdot q_{c,t_{n}} }
	{ \sum p_{c,t_{0}} \cdot q_{c,t_{n}} }
$$
Where
- $P$ is the relative index of price levels at two periods.
- $c$ is a single good or service in the set of all goods, $C$.
- $t_{0}$ is the base period.
- $t_{n}$ the period for which the index is computed.
- $p_{c,t}$ is the prevailing price of $c$ in period $t$.
- $q_{c,t}$ is the quantity of $c$ sold in period $t$.

The Paasche index tends to **understate** inflation, because the indices do not account for the fact that consumers typically react to price changes by changing the quantities that they buy 

## The Laspeyres Index
Almost identical to the Paasche method in form and popularity, but uses quantities from $t_{0}$ instead of $t_{n}$. 
$$
P_{p} = \frac
	{ \sum p_{c,t_{n}} \cdot q_{c,t_{0}} }
	{ \sum p_{c,t_{0}} \cdot q_{c,t_{0}} }
$$
The Laspeyres index tends to **overstate** inflation.

## The Tornqvist Index

## The Fisher Index

## The Divisia Index
This index has been around since the 1920s, but economists have never been comfortable with it because it introduces [[Path Dependence]], which they see as a flaw.

Physicists learn to love path dependence once they realized the role that it was playing.

## Ragnar Frisch's Theorem
In 1930, Ragnar Frisch proves that there is no index number that can satisfy the 3 so-called Fisher Axioms. Note that $p^{0} = p^{1}$ yields 1 in all cases but the last.