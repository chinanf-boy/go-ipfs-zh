## 测试命令覆盖率,清晰度(Sharness)

| 模块      | 在线(online)测试 | 离线测试    |
| --------- | ---------------- | ----------- |
| object    | t0051            | t0051       |
| ls        | t0045            | t0045       |
| cat       | t0040            |             |
| dht       |                  |             |
| bitswap   |                  |             |
| block     |                  | t0050       |
| daemon    | t0030            | (N/A)不适用 |
| init      | N/A              | t0045       |
| add       | t0040            |             |
| config    | t0021            | t0021       |
| version   | t0060            | t0010       |
| ping      |                  |             |
| diag      |                  |             |
| mount     | t0030            |             |
| name      | t0110            | t0100       |
| pin       | t0080            |             |
| get       | t0090            | t0090       |
| refs      | t0080            |             |
| repo GC   | t0080            |             |
| id        |                  |             |
| bootstrap | t0120            | t0120       |
| swarm     |                  |             |
| update    |                  |             |
| commands  |                  |             |
