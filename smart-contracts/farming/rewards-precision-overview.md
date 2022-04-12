# Rewards precision overview

Rewards precision consists of 18 decimal places. This is done to improve the accuracy of the rewards calculation. When an admin setups a reward per second, he should add 18 extra symbols (multiply by 10^18). For example:

* 2 tokens per second → 2 \* 10^18 -> 2000000000000000000;
* 5.5 tokens per second → 5.5 \* 10^18 -> 5500000000000000000;
* 12.999 tokens per second → 12.999 \* 10^18 -> 12999000000000000000.
