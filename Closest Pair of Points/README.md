# Closest Pair of Points

We now consider the problem of finding the closest pair of points in a set $Q$ of $n \geq 2$ points. “Closest” refers to the usual euclidean distance: the distance between points $p_1 = (x_1; y_1)$ and $p_2 = (x_2; y_2)$ is $\sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$.

## The divide-and-conquer algorithm

Each recursive invocation of the algorithm takes as input a subset $P \subseteq Q$ and arrays $X$ and $Y$, each of which contains all the points of the input subset $P$. The points in array $X$ are sorted so that their $x$-coordinates are monotonically increasing. Similarly, array $Y$ is sorted by monotonically increasing $y$-coordinate.

A given recursive invocation with inputs $P$, $X$, and $Y$ first checks whether
$|P| \leq 3$. If so, the invocation simply performs the brute-force method. If $|P| \gt 3$, the recursive invocation carries out the divide-and-conquer paradigm as follows.

- **Divide:** Find a vertical line $l$ that bisects the point set $P$ into two sets $P_L$ and $P_R$ such that $|P_L| = \lceil|P|/2\rceil$, $|P_R| = \lfloor|P|/2\rfloor$, all points in $P_L$ are on or to the left of line $l$, and all points in $P_R$ are on or to the right of $l$. Divide the array $X$ into arrays $X_L$ and $X_R$, which contain the points of $P_L$ and $P_R$ respectively, sorted by monotonically increasing $x$-coordinate. Similarly, divide the array $Y$ into arrays $Y_L$ and $Y_R$, which contain the points of $P_L$ and $P_R$ respectively, sorted by monotonically increasing $y$-coordinate.

- **Conquer:** Having divided $P$ into $P_L$ and $P_R$, make two recursive calls, one to find the closest pair of points in $P_L$ and the other to find the closest pair of points in $P_R$. The inputs to the first call are the subset $P_L$ and arrays $X_L$ and $Y_L$; the second call receives the inputs $P_R$, $X_R$, and $Y_R$. Let the closest-pair distances returned for $P_L$ and $P_R$ be $\delta_L$ and $\delta_R$, respectively, and let $\delta = min(\delta_L, \delta_R)$.

- **Combine:** The closest pair is either the pair with distance $\delta$ found by one of the recursive calls, or it is a pair of points with one point in $P_L$ and the other in $P_R$. The algorithm determines whether there is a pair with one point in $P_L$ and the other point in $P_R$ and whose distance is less than $\delta$. Observe that if a pair of points has distance less than $\delta$, both points of the pair must be within $\delta$ units of line $l$. To find such a pair, if one exists, we do the following:

    1. Create an array $Y'$, which is the array $Y$ with all points not in the $2\delta$-wide vertical strip removed. The array $Y'$ is sorted by $y$-coordinate, just as $Y$ is.

    2. For each point p in the array $Y'$, try to find points in $Y'$ that are within $\delta$ units of $p$. As we shall see shortly, only the 7 points in $Y'$ that follow $p$ need be considered. Compute the distance from $p$ to each of these 7 points, and keep track of the closest-pair distance $\delta'$ found over all pairs of points in $Y'$.

    3. If $\delta' < \delta$, then the vertical strip does indeed contain a closer pair than the recursive calls found. Return this pair and its distance $\delta'$. Otherwise, return the closest pair and its distance $\delta$ found by the recursive calls.

## Bibliography

*Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2022). Introduction to algorithms. MIT press.*