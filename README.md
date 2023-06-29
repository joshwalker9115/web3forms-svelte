
[![Web3forms](https://web3forms.com/img/web3forms-logo.svg)](https://web3forms.com/)[![Svelte](https://avatars.githubusercontent.com/u/23617963?s=48&v=4)](https://svelte.dev)
# Web3forms Svelte component 📦

Recieve form submissions directly to your inbox without any configuration. Powered by Web3forms.

[![NPM](https://img.shields.io/npm/v/web3forms-svelte.svg)](https://www.npmjs.com/package/web3forms-svelte)
![Downloads](https://badgen.net/npm/dw/web3forms-svelte)
![Size without zipping](https://badgen.net/bundlephobia/min/web3forms-svelte)
![Size with zipping](https://badgen.net/bundlephobia/minzip/web3forms-svelte)
![Zero dependencies](https://badgen.net/bundlephobia/dependency-count/web3forms-svelte)
![License](https://badgen.net/npm/license/web3forms-svelte)
![Types included](https://badgen.net/npm/types/web3forms-svelte)
## Features ✨

✅  Super lightweight  
✅  Zero dependencies  
✅  Full Typescript support  
✅  Easy to use and a simple Access key   
✅  No configuration required (except for the Access key)  
- [ ] Examples  

## Demo

Checkout the demo in the [Svelte REPL](https://svelte.dev/repl/9755e377825d4d46bbbca3f70ed7c8b6?version=4.0.1)


## Installation

First get your Web3forms access from [here](https://web3forms.com/#start). And then👇

```bash
npm i web3forms-svelte
```
And for yarn users👇
```bash
yarn add web3forms-svelte
```
> Also please do note that the Web3forms Access key can be shared in public (just like the firebase keys).

## Usage 📖

```svelte
<script>
	import Web3Form from 'web3forms-svelte';
</script>

<Web3Form apikey="your-api-key-goes-here" />
```
For the full guide to props & usage checkout the [Design Doc](https://github.com/joshwalker9115/web3forms-svelte/tree/main/DESIGN_DOC.md).

<!-- For other examples please look at the [example page](https://github.com/joshwalker9115/web3forms-svelte/tree/main/src/routes/+page.svelte). -->

---
## FAQ ❓

#### Should I have a Web3forms account to use this library?  
You should get your Access key from [Web3forms](https://web3forms.com/) which requires your email.

#### How many form submissions can I make?  
Web3forms has a generous free plan. You can view the latest pricing [here](https://web3forms.com/#pricing).

## Run Locally

Clone the project

```bash
git clone https://github.com/joshwalker9115/web3forms-svelte.git
```

Go to the project directory

```bash
cd web3forms-svelte
```

Install dependencies

```bash
npm install
```
or
```bash
yarn
```

Start the server

```bash
npm run dev
```
or
```bash
yarn dev
```


  