Suppose we have a simple betting game where a single player bets on whether a coin flip will produce heads or tails. More specifically, the game is divided into $n$ rounds ($1 \\leqslant n \\leqslant 1,000$), where the money available at the start of each round is denoted as $m\_ i$ and the bet amount is denoted as $b\_ i$. The outcome of each round is determined by the flip of a fair coin. The rules of the game are as follows:

*   $1 \\leqslant m\_1 \\leqslant 1,000$  
    Players must start the game with at least $1 and at most $1,000.
    
*   $1 \\leqslant b\_ i \\leqslant m\_ i$  
    On any given round, you can’t bet more money than you have at the start of that round.
    
*   If the outcome of round $i$ is heads, then $m\_{i+1} = m\_ i + b\_ i$.
    
*   If the outcome of round $i$ is tails, then $m\_{i+1} = m\_ i \- b\_ i$.
    
*   The game ends once all $n$ rounds have been played or if, in any given round $i$, $m\_ i = 0$ (the player is broke and can’t continue playing).
    

In the 18th century, French gamblers tried to come up with a winning strategy for this game and others with similar rules. They came up with a strategy called the _martingale_, where the player chooses an initial bet $b\_1$ and then updates $b\_ i$ in subsequent rounds based on the result of the previous round. More specifically:

*   If the player lost round $i$ (i.e., the coin flip produced tails), then $b\_{i+1} = \\min (2\\cdot b\_ i, m\_{i+1})$.
    
*   If the player won round $i$ (i.e., the coin flip produced heads), then $b\_{i+1} = \\min (b\_1, m\_{i+1})$.
    

The intuition behind this strategy is the following: if you lose a round, you want to recover those loses _and_ still make a profit if you win the next round, so you double the bet amount (without exceeding the amount of money on hand). However, once you win a round, you want to return to a less aggressive betting strategy, and return to betting the initial bet amount $b\_1$ (without exceeding the amount of money on hand).

For example, if you had $100 and bet $20, but lost the bet, you would be left with $80. According to the martingale rules, you would now bet $40 and, if you won, you would have $120 (you recovered your loses and made an extra $20). Of course, if you lost the second round too, you would be down to $40.

Here is a more complete example, for a game with $n=4$ rounds, $m\_1=100$, and $b\_1=5$.

$i$

$m\_ i$

$b\_ i$

Coin Flip

$m\_{i+1}$

$b\_{i+1}$

Comments

1

100

5

TAILS

95

10

We double the bet amount.

2

95

10

HEADS

105

5

We go back to betting $b\_1$.

3

105

5

TAILS

100

10

We double the bet amount again.

4

100

10

TAILS

90

—

Last round. The game ends here.

At the end of this game, the player has $90.

Here is a different example, where the player ends up going broke ($n=8$, $m\_1=140$, $b\_1=20$).

$i$

$m\_ i$

$b\_ i$

Coin Flip

$m\_{i+1}$

$b\_{i+1}$

Comments

1

140

20

TAILS

120

40

We double the bet amount.

2

120

40

TAILS

80

80

We double the bet amount again.

3

80

80

TAILS

0

—

The player is broke. The game ends here.

Notice how, even though the game had more rounds, the game ends after the third round because the player has no more money to bet.

So, although the martingale strategy can be effective in quickly recovering from a loss, it can also make the player go broke much faster. In fact, it has been shown that a martingale strategy can only be effective with infinite wealth and time.

You will write a program that, given values for $n$, $m\_1$, and $b\_1$, will compute the outcome of the game according to the martingale betting strategy described above.

Input
-----

The input contains the specification of a single game. The first three lines contain the values of $m\_1$, $b\_1$, and $n$, respectively. The fourth line contains $n$ integers, each separated by a single space. These integers specify the outcome of the $n$ coin flips in the game: a 1 indicates heads, and a 0 indicates tails.

Note that the first two sample inputs correspond to the two examples shown above.

Output
------

The output contains a single line with the result of the game. If the player goes broke, print BROKE. Otherwise, print a single integer with the amount of money that the player has at the end of the game (i.e., $m\_{n+1}$)

Sample Input 1

Sample Output 1

100
5
4
0 1 0 0

90

Sample Input 2

Sample Output 2

140
20
8
0 0 0 1 0 1 1 1

BROKE

Sample Input 3

Sample Output 3

100
5
4
1 1 1 1

120
