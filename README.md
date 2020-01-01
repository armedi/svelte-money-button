Svelte Money Button is a Svelte component that lets you integrate [Money Button](https://moneybutton.com)’s payment system into your app with only a few lines of code.

## Installation

Svelte Money Button is available on the npm registry. You can install it both via yarn and npm.

```sh
yarn add svelte-money-button
# or
npm install svelte-money-button
```

## Getting started

Using Svelte Money Button is as simple as adding this component to your app:

```html
<script>
  import MoneyButton from "svelte-money-button";
</script>

<div>
  <MoneyButton
    to="<your-bitcoin-address-here>"
    amount="1"
    currency="USD"
  />
</div>
```

It accepts all props similar to it's React counterpart. For the official React library check out the [docs](https://docs.moneybutton.com/docs/mb-react.html).

