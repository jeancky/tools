## Awesome Tools

This repo contains some useful sub commands for ethereum and TRON

## Sub commands

| Command | Description                                 |
|:-------:|---------------------------------------------|
|  `db`   | Database related commands                   |
| `addr`  | Address related commands                    |
|  `vm`   | EVM related commands                        |
| `scan`  | TronScan related commands                   |
|  `eth`  | ETH JSON-RPC related commands               |
|  `now`  | Convert time between datetime and timestamp |
|  `hex`  | Convert num between decimal and hexadecimal |

## Installation

```shell
protoc --go_out=./proto ./proto/*.proto
go build -o /usr/local/bin/tools
ln -s /usr/local/bin/tools /bin/tt
```

### How to install `protoc` or `go`

Can't you fucking Google it?

## Commands Usage

### db subcommands

```shell
$ tt db
NAME:
   tt db - Database related commands

USAGE:
   tt db command [command options] [arguments...]

COMMANDS:
   count  Count the total items for given name db
   get    Get value of the given key in db
   hash   Calculate the hash for given name db
   print  Print all key-value for given name db
   diff   Diff for given db-A and db-B

OPTIONS:
   --help, -h  show help (default: false)
```

### `addr` subcommands

```shell
$ tt addr
NAME:
   tt addr - Address related commands

USAGE:
   tt addr command [command options] [arguments...]

COMMANDS:
   num     Pad the given num to address
   decode  Decode base58 encoded address to eth address
   encode  Encode eth address to base58 encoded address

OPTIONS:
   --help, -h  show help (default: false)
```

#### examples

```shell
$ tt addr num 0
0x0000000000000000000000000000000000000000
T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb

$ tt addr num 1
0x0000000000000000000000000000000000000001
T9yD14Nj9j7xAB4dbGeiX9h8unkKLxmGkn

$ tt addr decode TDpt9adA6QidL1B1sy3D8NC717C6L5JxFo
0x2A4D700C196a78F8ff7F0bf17d93Fe6018396d2E

$ tt addr encode 0x78880fbe59623b0961a9999faa48dc000b8f97df
TLxX5oCK76yMHJ2r9TSrQHK44j1bUCxkP5
```

### `vm` subcommands

```shell
$ tt vm
NAME:
   tt vm - EVM related commands

USAGE:
   tt vm command [command options] [arguments...]

COMMANDS:
   pad     Pad num(in hex or dec) to 32bytes
   split   Spilt data to each 32bytes
   unpack  Unpack data with given types
   4bytes  Get 4bytes selector for given func or event

OPTIONS:
   --help, -h  show help (default: false)
```

#### examples

```shell
$ tt vm pad 0
[origin hex] 0x
[padded hex] 0x0000000000000000000000000000000000000000000000000000000000000000

$ tt vm pad 100
[origin hex] 0x64
[padded hex] 0x0000000000000000000000000000000000000000000000000000000000000064

$ tt vm pad 0xdead
[padded hex in big endian] 0x000000000000000000000000000000000000000000000000000000000000dead
[padded hex in little endian] 0xdead000000000000000000000000000000000000000000000000000000000000

$ tt vm split 000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000b1a2bc2ec500000000000000000000000000000000000000000000000000000f207539952d00000000000000000000000000000000000000000000000000000b1a2bc2ec500000000000000000000000000041aa6f10960ed9f7fe44aacc3aa33dd8f7da108c23
[each data word]:
0x00: 0000000000000000000000000000000000000000000000000000000000000000
0x20: 00000000000000000000000000000000000000000000000000b1a2bc2ec50000
0x40: 0000000000000000000000000000000000000000000000000f207539952d0000
0x60: 0000000000000000000000000000000000000000000000000b1a2bc2ec500000
0x80: 000000000000000000000041aa6f10960ed9f7fe44aacc3aa33dd8f7da108c23

$ tt vm unpack "address,address,address,address" 000000000000000000000000e3a2cdc25058e5dee0f4b5c1d5c7bfd5dd6836be000000000000000000000000cd420bb0b2b3fd8fa65cb53e01d47738d27949430000000000000000000000008086b67a46a54c7b42d90107e795d3e3c92f6d2100000000000000000000000065fa68800fff5a10346d1a3aa1fb2ce92f2e2971
[unpack result]:
  - [arg-00]: address, 0xe3a2CDC25058e5DEe0F4b5C1d5C7BFD5DD6836Be - TWiqRQZkKqPFV6saFw9dqHJrNG64f7QCPw
  - [arg-01]: address, 0xCd420BB0B2B3FD8Fa65Cb53e01d47738D2794943 - TUgWeKNGt22aig8YRYVAhBFnBK22A2WuZ4
  - [arg-02]: address, 0x8086B67a46a54C7b42D90107e795d3e3C92F6D21 - TMgnsd5t6516yy4xcgod251oSFWcrmWAUo
  - [arg-03]: address, 0x65fA68800FFf5A10346D1A3aA1fb2Ce92f2E2971 - TKGRE6oiU3rEzasue4MsB6sCXXSTx9BAe3

$ tt vm unpack "uint256,uint256,uint256,uint256,address" 00000000000000000000000000000000000000000000000000470de4df8200000000000000000000000000000000000000000000000000000429d069189e00000000000000000000000000000000000000000000000000003782dace9d9000000000000000000000000000000000000000000000000000000b1a2bc2ec50000000000000000000000000004134a0f029365c5a6af762fa14d7638a583f72595b
[unpack result]:
  - [arg-00]: uint256, 20000000000000000 - 20,000,000,000,000,000 (17)
  - [arg-01]: uint256, 300000000000000000 - 300,000,000,000,000,000 (18)
  - [arg-02]: uint256, 4000000000000000000 - 4,000,000,000,000,000,000 (19)
  - [arg-03]: uint256, 800000000000000000 - 800,000,000,000,000,000 (18)
  - [arg-04]: address, 0x34A0F029365c5a6aF762FA14D7638a583f72595b - TEmUwDDSPDF6ajToBm2QDg4p3WJUVjYZ4i

$ tt vm unpack "uint256[],uint256[],uint256[],uint256[]" 000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000004119011a363613ee4800000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000056bc75e2d6310000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000de1a4662fd0beb000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000de1b9f3e061d692
[unpack result]:
  - [arg-00]: uint256[]
    - [slice-00]: uint256, 1200840114937183596104 - 1,200,840,114,937,183,596,104 (22)
  - [arg-01]: uint256[]
    - [slice-00]: uint256, 100000000000000000000 - 100,000,000,000,000,000,000 (21)
  - [arg-02]: uint256[]
    - [slice-00]: uint256, 1000261351048789680 - 1,000,261,351,048,789,680 (19)
  - [arg-03]: uint256[]
    - [slice-00]: uint256, 1000285049345660562 - 1,000,285,049,345,660,562 (19)

$ tt vm 4bytes 'regUser(address,string)'
[origin hex] 0x5a7c7895
[padded hex] 0x5a7c789500000000000000000000000000000000000000000000000000000000
```

### `scan` subcommands

```shell
$ tt scan
NAME:
   tt scan - TronScan related commands

USAGE:
   tt scan command [command options] [arguments...]

COMMANDS:
   txs       Query txs in the given net for the given account
   tx        Query the tx in the given net for the given tx hash
   speed     Query pool speed for given token
   transfer  Query all transfer records for given pool

OPTIONS:
   --help, -h  show help (default: false)
```

#### examples

```shell
$ tt scan txs main TY5cfgCous8GH7rXUrNjRydTMkVHR2BNsR 0 50
[Legend]: ✅ - [Success] ⚠️  - [Revert] ⏱  - [Out_Of_Time] ⚡️ - [Out_Of_Energy] 💢 - [Other]
 1 2022-06-28 20:00:15 ab883582c7ee85d2ed1376e5c187f953c43bec984699a91555f0f8728e5e926e TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 2 2022-06-28 20:00:09 ca6c1b892c8174a9df81cef8335f904c2ef8d13bed40c36d519e8e08de743768 TWKnrGqU5dijnWT7dbPCDZV23C622T5FDv ✅ getReward()
 3 2022-06-27 20:00:09 c8973f4c4435b816ea98ca66dc7c8d8443d920ab9dde1b7f052796bd28bb40ff TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 4 2022-06-26 20:00:09 b7c43da37f5ece68c6df042bca478e908894a6f662844140f60e6bb56d7d28d3 TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 5 2022-06-25 20:00:09 1777e6b96ba06f19eafc6345694841917106e49a44747e607c1b52e3ab51396e TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 6 2022-06-24 20:00:09 bab6d8ac4ce421f61a0a58dd13f2ad1d4410598a5d68a8cd843711399e459064 TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 7 2022-06-23 20:18:00 f7f33e53df3040d710da6041dbf16e0679d21a321c2155ccee52258d4fb0213e TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 8 2022-06-22 20:00:09 dc3efc5f33741cea12898f4eb66c089dd469f08e4f580d0839fa4494dd99d7e1 TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 9 2022-06-21 20:00:09 ac6951c2c1c836311a0ebd6497fd5a27e0a8df69fd46e6a182cc11740f139fd4 TAFotzexiiUJzGkBHDy9Jbn7rVHoYyWuLA ✅ getReward()
 ...

$ tt scan tx main 4b1118a8303b23e2ef8ddd9b6b6ce5de2638f18f1d03435e692fc01e3254fd20
[Return data]:
  - In HEX: 08C379A00000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000A6C6F772072657475726E00000000000000000000000000000000000000000000
  - In ASCII:�y�
low return
[From]: TGaXLDXtndZwrjrCSdaByqXubfbE1NdbqU
[To]: TP2igjG2ofLq495iz6fW93JrzeVTZRfRA6
[Method]: mine_route_u_three(address[] _tokenIn,uint256 _amountIn,uint256[] _route,uint256 _minReturn)
  - [Arg-00]: address[]
    - [slice-00]: address, 0x891cdb91d149f23B1a45D9c5Ca78a88d0cB44C18 - TNUC9Qb1rRpS5CbWLmNMxXBjyFoydXjWFR
    - [slice-01]: address, 0x0Efac3802727c5F873b887e8119fe895B5156577 - TBLQs7LqUYAgzYirNtaiX3ixnCKnhrVVCe
    - [slice-02]: address, 0xa614f803B6FD780986A42c78Ec9c7f77e6DeD13C - TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t
    - [slice-03]: address, 0x891cdb91d149f23B1a45D9c5Ca78a88d0cB44C18 - TNUC9Qb1rRpS5CbWLmNMxXBjyFoydXjWFR
  - [Arg-01]: uint256, 3209302261 - 3,209,302,261 (10)
  - [Arg-02]: uint256[]
    - [slice-00]: uint256, 30
    - [slice-01]: uint256, 14
    - [slice-02]: uint256, 12
  - [Arg-03]: uint256, 3209302261 - 3,209,302,261 (10)


```

### `eth` subcommands

```shell
$ tt eth
NAME:
   tt eth - ETH JSON-RPC related commands

USAGE:
   tt eth command [command options] [arguments...]

COMMANDS:
   logs  Query eth logs with given address, from block and topics, `page` logs at a query

OPTIONS:
   --help, -h  show help (default: false)
```

#### examples

```shell
$ tt eth logs 0x0a3f6849f78076aefaDf113F5BED87720274dDC0 14000000 0x3c278bd500000000000000000000000000000000000000000000000000000000 100000
[████████████████████████████████████████████████████████████████████████████████████████████████████] 100%    3m 47s   1042429/1042429
{"address":"0x0a3f6849f78076aefadf113f5bed87720274ddc0","topics":["0x3c278bd500000000000000000000000000000000000000000000000000000000","0x0000000000000000000000005cab1e5286529370880776461c53a0e47d74fb63","0x000000000000000000000000dd5052bfc4d281793653b0037d46cc2d8d1fd1b5","0x0000000000000000000000000000000000000000000000000000000000000000"],"data":"0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000243c278bd5000000000000000000000000dd5052bfc4d281793653b0037d46cc2d8d1fd1b500000000000000000000000000000000000000000000000000000000","blockNumber":"0xd5bb8f","transactionHash":"0xf8ac4aa71470b2e43fc1c3dbb5a57530a1aa16eee3d16eaad491316321107f03","transactionIndex":"0x19","blockHash":"0xc67969a6d668e7aeef65d8b7c18be55dece2c8ba6f10291bc2a3ee144384fedb","logIndex":"0x19","removed":false}
{"address":"0x0a3f6849f78076aefadf113f5bed87720274ddc0","topics":["0x3c278bd500000000000000000000000000000000000000000000000000000000","0x0000000000000000000000005cab1e5286529370880776461c53a0e47d74fb63","0x000000000000000000000000e246c4ba65d95c2f902e39fbeb0047a67ab4f25a","0x0000000000000000000000000000000000000000000000000000000000000000"],"data":"0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000243c278bd5000000000000000000000000e246c4ba65d95c2f902e39fbeb0047a67ab4f25a00000000000000000000000000000000000000000000000000000000","blockNumber":"0xd6800c","transactionHash":"0x6718672e2e53b2581d94ed0e0e9580347298f9c3745220c4dca74028e309350c","transactionIndex":"0x15c","blockHash":"0x0c8c355eb711811c9f9db809a6ec3a2934a6d1bb283b268efd0b0da7b6ef5f18","logIndex":"0x244","removed":false}
```

### `now` command

#### examples

```shell
$ tt now
1659077089
1659077089778
2022-07-29 14:44:49
$ tt now 1659077089
2022-07-29 14:44:49
$ tt now 2022-07-29
1659024000
$ tt now '2022-07-29 14:44:49'
1659077089
```

### `hex` command

#### examples

```shell
$ tt hex 0x0200007368616269
[in decimal] - 144115683748307561
[in ascii]   - shabi
$ tt hex 1000000000000000000
[in hex] - 0x0de0b6b3a7640000
```