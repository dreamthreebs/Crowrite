# 0409-neovim-config

## Basic config

<pre class="language-lua"><code class="lang-lua"><strong>vim.api.nvim_set_keymap("i", "jk", "&#x3C;Esc>", { noremap = true, silent = true })
</strong>
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

if vim.g.neovide then
  vim.g.neovide_cursor_vfx_mode = { "railgun", "ripple" }
end
</code></pre>

## Avante.nvim

```
return {
  {
    "yetone/avante.nvim",
    event = "VeryLazy",
    lazy = false,
    version = false, -- set this if you want to always pull the latest change
    opts = {
      provider = "deepseek",
      vendors = {
        deepseek = {
          __inherited_from = "openai",
          api_key_name = "OPENAI_API_KEY",
          endpoint = "https://api.deepseek.com",
          model = "deepseek-coder",
          max_tokens = 8192,
        },
        paoluz = {
          api_key_name = "PAOLUZ_API_KEY",
          endpoint = "https://chatapi.nloli.xyz",
          model = "gpt-4o",
          max_tokens = 8192,
        },
      },
    },
    -- if you want to build from source then do `make BUILD_FROM_SOURCE=true`
    build = "make",
    -- build = "powershell -ExecutionPolicy Bypass -File Build.ps1 -BuildFromSource false" -- for windows
    dependencies = {
      "nvim-treesitter/nvim-treesitter",
      "stevearc/dressing.nvim",
      "nvim-lua/plenary.nvim",
      "MunifTanjim/nui.nvim",
      --- The below dependencies are optional,
      "nvim-tree/nvim-web-devicons", -- or echasnovski/mini.icons
      "zbirenbaum/copilot.lua", -- for providers='copilot'
      {
        -- support for image pasting
        "HakonHarnes/img-clip.nvim",
        event = "VeryLazy",
        opts = {
          -- recommended settings
          default = {
            embed_image_as_base64 = false,
            prompt_for_file_name = false,
            drag_and_drop = {
              insert_mode = true,
            },
            -- required for Windows users
            use_absolute_path = true,
          },
        },
      },
      {
        -- Make sure to set this up properly if you have lazy=true
        "MeanderingProgrammer/render-markdown.nvim",
        opts = {
          file_types = { "markdown", "Avante" },
        },
        ft = { "markdown", "Avante" },
      },
    },
  },
}
```
