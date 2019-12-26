# GetBlockValue @ main.cpp:675

```
int64 CBlock::GetBlockValue(int64 nFees) const
{
    int64 nSubsidy = 50 * COIN;

    // Subsidy is cut in half every 4 years
    nSubsidy >>= (nBestHeight / 210000);

    return nSubsidy + nFees;
}
```

Bitcoins are created each time a user discovers a new block. The rate of block creation is adjusted every 2016 blocks to aim for a constant two week adjustment period (equivalent to 6 per hour.) The number of bitcoins generated per block is set to decrease geometrically, with a 50% reduction every 210,000 blocks, or approximately four years. The result is that the number of bitcoins in existence will not exceed slightly less than 21 million.

![Controlled Supply](https://en.bitcoin.it/w/images/en/e/e0/Controlled_supply-block_reward_halving.png)

Speculated justifications for the unintuitive value "21 million" are that it matches a 4-year reward halving schedule; or the ultimate total number of Satoshis that will be mined is close to the maximum capacity of a 64-bit floating point number. Satoshi has never really justified or explained many of these constants.


> A fixed money supply, or a supply altered only in accord with objective and calculable criteria, is a necessary condition to a meaningful just price of money.

—Fr. Bernard W. Dempsey, S.J. (1903-1960)


### Example in python
```
COIN = 100 * 1000 * 1000
nSubsidy = 50 * COIN
nHeight = 0
total = 0
while nSubsidy != 0:
    nSubsidy = 50 * COIN
    nSubsidy >>= nHeight / 210000
    nHeight += 1
    total += nSubsidy

print total / float(COIN)

```
