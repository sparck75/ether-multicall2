# ethers-multicall2

Make multiple Ethereum network requests in a single HTTP query. [ethcall](https://github.com/Destiner/ethcall) for ethers v5.

** adding support for multicall2 contract ... under development.

## API

* `Contract(address, abi)`: Create contract instance; calling `contract.callFuncName` will yield a `call` object
* `all(calls)`: Execute all calls in a single request
* `calls`: List of helper call methods
* `getEthBalance(address)`: Returns account ether balance

## Example

```ts
import { Contract, Provider } from 'ethers-multicall';
import { ethers } from 'ethers';

import erc20Abi from './abi/erc20.json';

const infuraKey = 'INSERT_YOUR_KEY_HERE';
const provider = new ethers.providers.InfuraProvider('mainnet', infuraKey);

const daiAddress = '0x6b175474e89094c44da98b954eedeac495271d0f';

async function call() {
  const ethcallProvider = new Provider(provider);

  await ethcallProvider.init(); // Only required when `chainId` is not provided in the `Provider` constructor

  const daiContract = new Contract(daiAddress, erc20Abi);

  const uniswapDaiPool = '0x2a1530c4c41db0b0b2bb646cb5eb1a67b7158667';

  const ethBalanceCall = ethcallProvider.getEthBalance(uniswapDaiPool);
  const daiBalanceCall = daiContract.balanceOf(uniswapDaiPool);

  const [ethBalance, daiBalance] = await ethcallProvider.all([ethBalanceCall, daiBalanceCall]);

  console.log('ETH Balance:', ethBalance.toString());
  console.log('DAI Balance:', daiBalance.toString());
}

call();
```
## Supported-Network
- Ethereum
- Binance Smart Chain
- Fantom
- Polygon
- Avalance
- and many more!


 | ChainId | Contract address                             |
 | 1       | 0xeefba1e63905ef1d7acba5a8513c70307c1ce441   |
 | 3       | 0xF24b01476a55d635118ca848fbc7Dab69d403be3   |
 | 4       | 0x42ad527de7d4e9d9d011ac45b31d8551f8fe9821   |
 | 5       | 0x77dca2c955b15e9de4dbbcf1246b4b85b651e50e   |
 | 42      | 0x2cc8688c5f75e365aaeeb4ea8d6a480405a48d2a   |
 | 56      | 0x1Ee38d535d541c55C9dae27B12edf090C608E6Fb   |
 | 66      | 0x94fEadE0D3D832E4A05d459eBeA9350c6cDd3bCa   |
 | 97      | 0x3A09ad1B8535F25b48e6Fa0CFd07dB6B017b31B2   |
 | 100     | 0xb5b692a88bdfc81ca69dcb1d924f59f0413a602a   |
 | 128     | 0x2C55D51804CF5b436BA5AF37bD7b8E5DB70EBf29   |
 | 137     | 0x11ce4B23bD875D7F5C6a31084f55fDe1e9A87507   |
 | 250     | 0x0118EF741097D0d3cc88e46233Da1e407d9ac139   |
 | 1337    | 0x77dca2c955b15e9de4dbbcf1246b4b85b651e50e   |
 | 42161   | 0x813715eF627B01f4931d8C6F8D2459F26E19137E   |
 | 43114   | 0x7f3aC7C283d7E6662D886F494f7bc6F1993cDacf   |
 | 80001   | 0x08411ADd0b5AA8ee47563b146743C13b3556c9Cc   |
