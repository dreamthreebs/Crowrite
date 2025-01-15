# 0115-file saving

```python
from pathlib import Path

# List of subdirectory names
subdirs = ['pcfn', 'cfn', 'cf', 'n', 'rmv', 'n_rmv', 'inp', 'n_inp']

# Base path
base_path = Path(f'./fit_res/sm/{sim_mode}')

# Create directories
for subdir in subdirs:
    (base_path / subdir).mkdir(exist_ok=True, parents=True)
```
