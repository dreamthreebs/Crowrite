# 0816-change $ to \$$

### CODE

find and substitude single `$` to double `$` &#x20;

```
from \$([^\$]+)\$ to $$$ $1 $$$
reverse substitude: \$\$ ([^\$]+)\$\$ to $$ $1 $$
```
