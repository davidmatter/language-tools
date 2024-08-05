# Vue Language Tools

> ⚡ High-performance Vue language tooling based-on [Volar.js](https://volarjs.dev/)

💬 **#language-tools** on our [Discord Server](https://discord.gg/vue)

## Example Projects

- [Basic Example](./examples/basic/) A basic example project that highlights some aspects of the Vue language tools. This example is a good starting point for new users.
- [[Todo] nvim](./examples/with-nvim/) If you are using Neovim, feel free to contribute an example project to help others.
- [[Todo] Vue2](./examples/with-vue2/) If you are using Vue 2, feel free to contribute an example project to help others.

## Packages

- [Vue Language Features](https://github.com/vuejs/language-tools/tree/master/extensions/vscode) \
  _Vue, Vitepress, petite-vue language support extension for VSCode_
- [vue-tsc](https://github.com/vuejs/language-tools/tree/master/packages/tsc) \
  _Type-check and dts build command line tool_
- [vue-component-meta](https://github.com/vuejs/language-tools/tree/master/packages/component-meta) \
  _Component props, events, slots types information extract tool_
- [vite-plugin-vue-component-preview](https://github.com/johnsoncodehk/vite-plugin-vue-component-preview) \
  _Vite plugin for support Vue component preview view with `Vue Language Features`_
- [`@vue/language-server`](/packages/language-server/) \
  _The language server itself_.
- [`@vue/typescript-plugin`](/packages/typescript-plugin/) \
  _Typescript plugin for the language server_.

## Community Integration

[yaegassy/coc-volar](https://github.com/yaegassy/coc-volar) ⚡ 🤝 🅿️ \
_Vue language client for coc.nvim_

[neovim/nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) ⚡ 🤝 \
_Vue language server configuration for Neovim_

<details>
  <summary>How to configure vue language server with neovim and lsp?</summary>

### Hybrid mode configuration (Requires `@vue/language-server` version `^2.0.0`)

Note: The "Take Over" mode has been discontinued. Instead, a new "Hybrid" mode has been introduced. In this mode, the Vue Language Server exclusively manages the CSS/HTML sections. As a result, you must run `@vue/language-server` in conjunction with a TypeScript server that employs `@vue/typescript-plugin`. Below is a streamlined configuration for Neovim's LSP, updated to accommodate the language server following the upgrade to version `2.0.0`.

```lua
-- If you are using mason.nvim, you can get the ts_plugin_path like this
-- local mason_registry = require('mason-registry')
-- local vue_language_server_path = mason_registry.get_package('vue-language-server'):get_install_path() .. '/node_modules/@vue/language-server'

local vue_language_server_path = '/path/to/@vue/language-server'

local lspconfig = require('lspconfig')

lspconfig.tsserver.setup {
  init_options = {
    plugins = {
      {
        name = '@vue/typescript-plugin',
        location = vue_language_server_path,
        languages = { 'vue' },
      },
    },
  },
  filetypes = { 'typescript', 'javascript', 'javascriptreact', 'typescriptreact', 'vue' },
}

-- No need to set `hybridMode` to `true` as it's the default value
lspconfig.volar.setup {}
```

### None-Hybrid mode(similar to takeover mode) configuration (Requires `@vue/language-server` version `^2.0.7`)

Note: If `hybridMode` is set to `false` `Volar` will run embedded `tsserver` therefore there is no need to run it separately.

For more information see [#4119](https://github.com/vuejs/language-tools/pull/4119)

_Make sure you have typescript installed globally or pass the location to volar_

Use volar for all `.{vue,js,ts,tsx,jsx}` files.

```lua
local lspconfig = require('lspconfig')

-- lspconfig.tsserver.setup {}
lspconfig.volar.setup {
  filetypes = { 'typescript', 'javascript', 'javascriptreact', 'typescriptreact', 'vue' },
  init_options = {
    vue = {
      hybridMode = false,
    },
  },
}
```

Use `volar` for only `.vue` files and `tsserver` for `.ts` and `.js` files.

```lua
local lspconfig = require('lspconfig')

lspconfig.tsserver.setup {
  init_options = {
    plugins = {
      {
        name = '@vue/typescript-plugin',
        location = '/path/to/@vue/language-server',
        languages = { 'vue' },
      },
    },
  },

lspconfig.volar.setup {
  init_options = {
    vue = {
      hybridMode = false,
    },
  },
},
```

### nvim-cmp integration

Check out this [discussion](https://github.com/vuejs/language-tools/discussions/4495)

</details>

[mattn/vim-lsp-settings](https://github.com/mattn/vim-lsp-settings) ⚡ \
_Vue language server auto configuration for vim-lsp_

[sublimelsp/LSP-volar](https://github.com/sublimelsp/LSP-volar) 🤝 \
_Vue language client for Sublime_

[kabiaa/atom-ide-volar](https://github.com/kabiaa/atom-ide-volar) \
_Vue language client for Atom_

[emacs-lsp/lsp-mode](https://github.com/emacs-lsp/lsp-mode) ([jadestrong/lsp-volar](https://github.com/jadestrong/lsp-volar)) ⚡ 🤝 \
_Vue language client for Emacs_

[tommasongr/nova-vue](https://github.com/tommasongr/nova-vue) \
_Vue language client for Nova_

[xiaoxin-sky/lapce-vue](https://github.com/xiaoxin-sky/lapce-vue) \
_Vue language client for Lapce_

[Kingwl/monaco-volar](https://github.com/Kingwl/monaco-volar) \
_Vue language support for Monaco on Browser_

[WebStorm](https://www.jetbrains.com/webstorm/) \
_Built-in integration for `@vue/language-server`_

[Eclipse WildWebDeveloper](https://github.com/eclipse-wildwebdeveloper/wildwebdeveloper) \
_Vue language server configuration for Eclipse_

\* ⚡ support [multiple servers](https://github.com/vuejs/language-tools/discussions/393#discussioncomment-1213736) \
\* 🤝 support [take over mode](https://github.com/vuejs/language-tools/discussions/471) \
\* 🅿️ support [extra preview features](https://twitter.com/johnsoncodehk/status/1507024137901916161)

<!-- Editor link: https://www.mermaidchart.com/app/projects/c62d8944-0e06-47f0-a8de-f89a7378490f/diagrams/91fd02c0-5c91-4f72-a8b4-7af21b7c4d86/version/v0.1/edit -->

<a href="https://www.mermaidchart.com/raw/91fd02c0-5c91-4f72-a8b4-7af21b7c4d86?theme=light&version=v0.1&format=svg">
	<img src="https://www.mermaidchart.com/raw/91fd02c0-5c91-4f72-a8b4-7af21b7c4d86?theme=light&version=v0.1&format=svg"/>
</a>

## Contribution Guide

If you want to work on the volar extension follow these commands to set up your local development environment.

🔎 Note that you will need pnpm - you can download it here: https://pnpm.io/installation.

```bash
git clone https://github.com/vuejs/language-tools.git
cd language-tools
pnpm install
pnpm run build
```

The recommended way to develop the volar extension is to use the [Debug Tools](https://code.visualstudio.com/Docs/editor/debugging) provided by VSCode.
Alternatively, you can run one of the scripts defined in the [package.json](https://github.com/vuejs/language-tools/blob/master/package.json) file.

❗ You should always use the debug launch configs or package.json scripts defined in the root of the project.

Additional info for contributing to open source projects can be found here: https://docs.github.com/en/get-started/quickstart/contributing-to-projects

To develop with upstream Volar.js modules, you can setup workspace with https://github.com/volarjs/workspace.

---

<h3 align="center">Full-time Support by</h3>
<br />

<p align="center">
	<span>
		<a href="https://stackblitz.com/">
			<img src="https://raw.githubusercontent.com/johnsoncodehk/sponsors/master/logos/StackBlitz.svg" height="80" />
			<h4 align="center">Boot a fresh environment in milliseconds.</h4>
		</a>
	</span>
</p>
<br />

<p align="center">
	<a href="https://cdn.jsdelivr.net/gh/johnsoncodehk/sponsors/sponsors.svg">
		<img src="https://cdn.jsdelivr.net/gh/johnsoncodehk/sponsors/sponsors.png"/>
	</a>
</p>
