<p align="center"><img src="vue-basqet.png?raw=true" width="70%"></p>

<br />

# Vue Component for Basqet

A Vue Plugin (Pay Button 💰) for Basqet payment gateway.  
It wraps the official [Basqet Web SDK](#);  
Making it pretty straightforward to add Basqet Pay Button to your vue-based application.
Available for Vue 2

## Installation

### NPM
```bash
npm install vue-basqet --save 
``` 
### Yarn
```bash
yarn add vue-basqet
``` 

### Javascript via CDN
```javascript 1.8
<!-- Vue -->
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<!-- Vue-Basqet -->
<script src="https://unpkg.com/vue-basqet/dist/vue-basqet.min.js"></script>
```

## Usage

```vue
<template>
    <vue-basqet
        ref="vueBasqetButton"
        :amount="amount"
        :public-key="basqetPublicKey"
        :email="email"
        :on-error="basqetError"
        :on-close="basqetClose"
        :on-success="basqetSuccess"
        :description="'Payment for service'"
    >
       Make Payment
    </vue-basqet>
</template>

<script type="text/javascript">
  import VueBasqet from 'vue-basqet';
  export default {
      components: {
          VueBasqet
      },
      
      data(){
          return{
            basqetPublicKey: process.env.BASQET_PUBLIC_KEY, // This has both test and product values
            email: "customer@domain.com", // Customer email
            amount: 10000 // of type:Number and in naira
          }
      },

      methods: {
        basqetSuccess: function(reference){
          // Perform other operations upon complete
          console.log("Basqet Payment Complete", reference)
        },
        basqetClose: function(){
          // Perform other operations upon close
          console.log("Basqet Payment Closed")
        },
        basqetError: function(error){
          // Perform other operations upon close
          console.log("Basqet Payment Failed", error)
        },
        // Handling click programmatically (Optional)
        handleBasqetClick: function() {
          this.$refs.vueBasqetButton.click()
        }
      }
  }
</script>
```

## For Nuxt
In /plugin/components.js
```javascript 1.8
import Vue from 'vue'
import VueBasqet from 'vue-basqet'

Vue.use('VueBasqet', VueBasqet)

// Other components package can be here too.
```

In nuxt.config.js
``` javascript 1.8
//...
plugins: [
  '@/plugins/components',
],
//...
```

In page or component as seen above (where it's used)  
You don't need to add: `import VueBasqet from 'vue-basqet';`

## All Props Available
```
publicKey: String (required)
email: String (required)
amount: Number (required)
onError: Function (required)
onClose: Function (required)
onSuccess: Function (required)
currency: String (optional) ['NGN']
description: String (optional) ['']
btnClass: String (optional)['']

i.e
// prop: DataType (required or optional) [default value]
```

## Contribution

Please feel free to fork this package and contribute by submitting a pull request to enhance the functionalities

## Appreciation

Give it a star and share the link to the repo on your social platforms.  
Thanks! Adedoyin Akande,  
Twitter: [@aeadedoyin ](https://twitter.com/aeadedoyin)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
