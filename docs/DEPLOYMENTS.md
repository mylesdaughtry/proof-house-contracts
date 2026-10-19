# Deployments

Proof House runs on **Ethereum mainnet, chain id 1**. Explorer: <https://etherscan.io>.

## How these addresses were checked

Each address below was checked against the chain on 2026-10-19:

1. it has contract code on chain 1;
2. its runtime bytecode matches a build of this repository at commit `a1735ce` (`forge build`: solc 0.8.26, `via_ir`,
   optimizer 200 runs, `evm_version = "cancun"`, `bytecode_hash = "none"`), with the constructor immutables masked
   out; for the seven contracts of the launch, IMD's published creation-code hashes match the same build;
3. the immutable wiring read from the contracts (for example `ArtifactsFactory.house()`,
   `ArtifactsPiece.keyProof()`, `BrokerPass`'s seats, factory and source) points at the other addresses in this file.

Owner, keeper and other wallet addresses are intentionally not listed here.

## The launch

Deployed by IMD's swarm in one transaction, IMD launch 2199, on 2026-10-19:
[`0x35159870…6e478`](https://etherscan.io/tx/0x351598706192e11dc7fbe2c40441c8e849d46fdc95e2fdf5ff8069dad23e6478)
(block 26224242, 15,209,172 gas), from commit `a1735ce` of
[identity-md-launches/launch-2199-deploy-proof-house-s-contracts](https://github.com/identity-md-launches/launch-2199-deploy-proof-house-s-contracts).

| Contract | Address | Source |
|---|---|---|
| ArtHouse (the ledger) | [`0x73b1e5825280df29ea7124e927f3ebd9710b5a99`](https://etherscan.io/address/0x73b1e5825280df29ea7124e927f3ebd9710b5a99) | `src/ArtHouse.sol` |
| ArtifactsFactory (the 255 editions) | [`0x62527f742de81a59e2bcd4d2633f796426553200`](https://etherscan.io/address/0x62527f742de81a59e2bcd4d2633f796426553200) | `src/ArtifactsFactory.sol` |
| ArtifactsSource (THE SOURCE and its auction) | [`0xe57e3f2ce296252b461911b34787371d6d806ab2`](https://etherscan.io/address/0xe57e3f2ce296252b461911b34787371d6d806ab2) | `src/ArtifactsSource.sol` |
| BrokerPass (100 free passes) | [`0xa6958cbc41325e97ecb3bb9d837fbd0938cb2b4f`](https://etherscan.io/address/0xa6958cbc41325e97ecb3bb9d837fbd0938cb2b4f) | `src/BrokerPass.sol` |
| SubmissionReviews | [`0xaa1142e3dc35d28cbf3a170bd931a76fc5b8aeab`](https://etherscan.io/address/0xaa1142e3dc35d28cbf3a170bd931a76fc5b8aeab) | `src/SubmissionReviews.sol` |
| KeyProof | [`0x2372c3081a910dd3dd7a3a3d6ec2427e2b30bd2f`](https://etherscan.io/address/0x2372c3081a910dd3dd7a3a3d6ec2427e2b30bd2f) | `src/KeyProof.sol` |
| ArtStorage | [`0x78d21b32dbd1bf216015b1dc4273072d3511bea7`](https://etherscan.io/address/0x78d21b32dbd1bf216015b1dc4273072d3511bea7) | `src/ArtStorage.sol` |
| ArtCollection implementation (created by ArtHouse's constructor) | [`0xa69dc7f635e9330b7964c80d1f798c950d60a90b`](https://etherscan.io/address/0xa69dc7f635e9330b7964c80d1f798c950d60a90b) | `src/ArtCollection.sol` |

## Deployed right after the launch

Outside IMD's launch transaction, which Ethereum caps at 16,777,216 gas (EIP-7825), from `launch.piece.json` and
`launch.burner.json`, on 2026-10-19.

| Contract | Address | Source |
|---|---|---|
| ArtifactsPiece (the locked implementation every piece is a full runtime copy of; set once on ArtifactsFactory and ArtifactsSource) | [`0x8b003b73cb5adeff29d27819e9953cdc9dd5a261`](https://etherscan.io/address/0x8b003b73cb5adeff29d27819e9953cdc9dd5a261) | `src/ArtifactsPiece.sol` |
| ImdBuybackBurner (ETH/IMD Uniswap v4 pool, fee 10000, tick spacing 200, no hook) | [`0x3d15de58d49af694236881403d9381d590008d1c`](https://etherscan.io/address/0x3d15de58d49af694236881403d9381d590008d1c) | `src/ImdBuybackBurner.sol` |

Each claimed edition, and THE SOURCE once settled, becomes its own ERC-721 contract, a copy of ArtifactsPiece. Find
them from ArtifactsFactory's `Claimed` events and `ArtifactsSource.pieceContract()`.

## External contracts it reads

| Contract | Address |
|---|---|
| IMD (ERC-20) | [`0xd34a99bc0f67ae1bbd63c660e6d0b0dd03e263b7`](https://etherscan.io/address/0xd34a99bc0f67ae1bbd63c660e6d0b0dd03e263b7) |
| identity.md seats (ERC-721) | [`0x0000ec93127baa929e58e97dd0095a2bfb38ec1d`](https://etherscan.io/address/0x0000ec93127baa929e58e97dd0095a2bfb38ec1d) |
| Cncptl Prspctv points (EngageV2), members count as holders | [`0x684a61e46ac3db9806a199bae7b9d456f525687d`](https://etherscan.io/address/0x684a61e46ac3db9806a199bae7b9d456f525687d) |
| Uniswap v4 PoolManager | [`0x000000000004444c5dc75cb358380d2e3de08a90`](https://etherscan.io/address/0x000000000004444c5dc75cb358380d2e3de08a90) |
| Multicall3 (read by the websites) | [`0xca11bde05977b3631167028862be2a173976ca11`](https://etherscan.io/address/0xca11bde05977b3631167028862be2a173976ca11) |
