# Closest Pair of Points

We now consider the problem of finding the closest pair of points in a set $Q$ of $n \geq 2$ points. “Closest” refers to the usual euclidean distance: the distance between points $p_1 = (x_1; y_1)$ and $p_2 = (x_2; y_2)$ is $\sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$.

## The divide-and-conquer algorithm

Each recursive invocation of the algorithm takes as input a subset $P \subseteq Q$ and arrays $X$ and $Y$, each of which contains all the points of the input subset $P$. The points in array $X$ are sorted so that their $x$-coordinates are monotonically increasing. Similarly, array $Y$ is sorted by monotonically increasing $y$-coordinate.

A given recursive invocation with inputs $P$, $X$, and $Y$ first checks whether
$|P| \leq 3$. If so, the invocation simply performs the brute-force method. If $|P| \gt 3$, the recursive invocation carries out the divide-and-conquer paradigm as follows.