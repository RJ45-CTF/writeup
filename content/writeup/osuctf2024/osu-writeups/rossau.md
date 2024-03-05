---
title: 'crypto/ROSSAU'
author: "nr1a"
---

```
My friend really likes sending me hidden messages, something about a public key with n = 5912718291679762008847883587848216166109 and e = 876603837240112836821145245971528442417. What is the name of player with the user ID of the private key exponent? (Wrap with osu{})
```

見れば誰でもわかる。これはRSAだ。

```
from sympy import *

# public key
n = 5912718291679762008847883587848216166109
e = 876603837240112836821145245971528442417

# prime factorization
p, q = factorint(n).keys()

# φ(n)
phi = (p - 1) * (q - 1)

# private key
d = pow(e, -1, phi)

print('https://osu.ppy.sh/users/' + str(d))
```

シンプルにcpuで計算させてuseridを取る。
そして問題文を見よう。
`What is the name of player with the user ID of the private key exponent?`
つまりflagはidっではなくプレイヤー名ということがわかる。

`flag: osu{chocomint}`
