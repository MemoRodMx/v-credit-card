## v-credit-card

Beautiful card form component for VueJS inspired by Adam Quinlan https://codepen.io/quinlo/pen/YONMEa

<img src="./card.gif">

#### Installation

```
npm install --save v-credit-card-mrodmx
```

#### usage

Register the component as a plugin and use it globally

```js
import Vue from "vue";
import VCreditCard from "v-credit-card-mrodmx";

Vue.component("v-credit-card", VCreditCard);

// usage
<v-credit-card />;
```

Or, import inside a component

```html
<template>
  <VCreditCard />
</template>

<script>
  import VCreditCard from "v-credit-card-mrodmx";

  export default {
    components: {
      VCreditCard,
    },
  };
</script>
```

#### Styles

You must import the CSS to get all the card styles

```js
import VCreditCard from "v-credit-card-mrodmx";
import "v-credit-card-mrodmx/dist/VCreditCard.css";
```

#### Available props

| props         | required | options      | default        | explenation                                       |
| ------------- | -------- | ------------ | -------------- | ------------------------------------------------- |
| direction     | no       | column, row  | row            | Card and form side-by-side or top to bottom       |
| className     | no       | any string   | none           | For any custom design, add your own wrapper class |
| yearDigits    | no       | 2,4 (number) | 2              | construct the expiration year (YY or YYYY)        |
| noCard        | no       | true, false  | false          | Show only the form without the credit card image  |
| trans         | no       | Object       | default labels | Override the default labels with your own         |
| nameMaxLength | no       | number       | 20             | Override the default name maxlength               |

#### Events

You can listen for the `@change` event to get an object of all the form fields with their current values

```html
<template>
  <VCreditCard @change="creditInfoChanged" />
</template>

<script>
  import VCreditCard from "v-credit-card";

  export default {
    // ...
    methods: {
      creditInfoChanged(values) {
        console.log("Credit card fields", values);
      },
    },
    components: {
      VCreditCard,
    },
  };
</script>
```

#### Example: store the form data in your component

This example shows how to have your local data reflect the changes inside the card component.

```html
<template>
  <VCreditCard @change="creditInfoChanged" />
</template>

<script>
  import VCreditCard from "v-credit-card";

  export default {
    data() {
      return {
        name: "",
        cardNumber: "",
        expiration: "",
        security: "",
      };
    },
    methods: {
      creditInfoChanged(values) {
        for (const key in values) {
          this[key] = values[key];
        }
      },
    },
    components: {
      VCreditCard,
    },
  };
</script>
```

If you need the card type as well (Visa, Mastercard, etc) you can listen to the `@cardChanged` event.

```html
<template>
  <VCreditCard @cardChanged="cardChanged" />
</template>

<script>
  import VCreditCard from "v-credit-card";

  export default {
    data() {
      return {
        // ...
        cardName: null,
      };
    },
    methods: {
      // ...
      cardChanged(cardName) {
        this.cardName = cardName;
      },
    },
    components: {
      VCreditCard,
    },
  };
</script>
```

#### Translations

If you wish to override the default field labels, you can accomplish that by passing a custom translation object.

```html
<template>
  <VCreditCard :trans="translations" />
</template>

<script>
  import VCreditCard from "v-credit-card";

  const translations = {
    name: {
      label: "Nombre",
      placeholder: "Nombre completo",
    },
    card: {
      label: "Número de tarjeta",
      placeholder: "Número de tarjeta",
    },
    expiration: {
      label: "Expiration",
    },
    security: {
      label: "Código de seguridad",
      placeholder: "Código",
    },
    year: {
      char: "Y",
    },
  };

  export default {
    data() {
      return {
        translations,
      };
    },
    components: {
      VCreditCard,
    },
  };
</script>
```

## License

MIT © 2018-present
