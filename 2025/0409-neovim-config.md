# 0409-neovim-config

```lua
vim.api.nvim_set_keymap("i", "jk", "<Esc>", { noremap = true, silent = true })

-- views can only be fully collapsed with the global statusline
vim.opt.laststatus = 3

local map = vim.keymap.set

-- Go to end of line
map("n", "sd", "$", { desc = "Go to end of line" })

-- Go to beginning of line
map("n", "sa", "0", { desc = "Go to beginning of line" })

-- Go to middle of screen line
map("n", "sw", "gM", { desc = "Go to middle of screen line" })

vim.g.mapleader = ","
```
