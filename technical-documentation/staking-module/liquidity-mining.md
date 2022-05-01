# Liquidity Mining

## C**ontract addresses**

| Name                   | Address                                    |
| ---------------------- | ------------------------------------------ |
| liquidityMiningManager | 0x21b56371c9D064Fe18cCa5798E164C25D73b9d36 |
| escrowPool             | 0xfEEA44bc2161F2Fe11D55E557ae4Ec855e2D1168 |
| mcPool                 | 0x5c76aD4764A4607cD57644faA937A8cA16729e39 |
| mcLPPool               | 0x44c01e5e4216f3162538914d9c7f5E6A0d87820e |
| view                   | 0xd191999c397d1D0ae6226d13547ca44378770b0F |

**The Merit Circle liquidity mining utilizes the following smart contracts**

`AbstractRewards.sol` is a generic contract for distributing pro-rata rewards amongst an arbitrary number of "shareholders", where the inheriting contract defines what a shareholder is and how many shares they have. This contract is a fork with minor modifications of the [<mark style="color:orange;">Indexed Finance contract</mark>](https://github.com/indexed-finance/dividends/blob/master/contracts/base/AbstractDividends.sol)<mark style="color:orange;">.</mark>

`BasePool.sol` is a generic ERC20 compatible contract which inherits from the ERC20Votes contract from OpenZeppelin and the `AbstractRewards.sol` contract and adds external functions for distributing and claiming rewards. Additionally it hooks into the internal `_transfer`, `burn`, and `mint` hooks to properly track rewards when account balances are changing.

`TokenSaver.sol` is a contract which allows a whitelisted address to transfer out any token out of a contract inheriting from it in case of emergencies or misplaced tokens.

`TimeLockPool.sol` Inherits from `BasePool.sol` and `TokenSaver.sol`. Adds external functions to deposit tokens and in return receive `TimeLockPool` shares. The bonus for longer locking durations is configurable.

`TimeLockNonTransferablePool.sol` inherits from `TimeLockPool.sol` and removes transferability of the pool shares.

`LiquidityMiningManager.sol` manages the distribution to staking pools. It exposes external functions which allow pools to be added and removed. It also allows the distribution per second to be set and the share each pool will receive of those rewards.

For further reading please see: [<mark style="color:orange;">https://github.com/Merit-Circle/merit-liquidity-mining</mark>](https://github.com/Merit-Circle/merit-liquidity-mining)<mark style="color:orange;"></mark>
