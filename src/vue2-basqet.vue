<template>
  <button :class="btnClass" @click="payWithBasqet">
      <slot>Make Payment</slot>
  </button>
</template>

<script>
export default {
  name: "VueBasqet", // vue component name
  props: {
    reference: {
      type: String,
      required: true,
    },
    publicKey: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    amount: {
      type: Number,
      required: true,
    },
    onSuccess: {
      type: Function,
      required: true,
      default(reference) {},
    },
    onError: {
      type: Function,
      required: true,
      default(error) {},
    },
    onClose: {
      type: Function,
      required: true,
      default() {},
    },
    currency: {
      type: String,
      default: "NGN",
    },
    description: {
      type: String,
      default: "",
    },
    btnClass: {
      type: String,
      default: "",
    },
  },

  data() {
    return {
      scriptLoaded: null,
    };
  },

  created() {
    this.scriptLoaded = new Promise((resolve) => {
      this.loadScript(() => {
        resolve();
      });
    });
  },

  methods: {
    loadScript(callback) {
      const script = document.createElement("script");
      script.src = "https://basqet-checkout.netlify.app/static/staging/basqet.js";
      document.getElementsByTagName("head")[0].appendChild(script);
      if (script.readyState) {
        // IE
        script.onreadystatechange = () => {
          if (
            script.readyState === "loaded" ||
            script.readyState === "complete"
          ) {
            script.onreadystatechange = null;
            callback();
          }
        };
      } else {
        // Others
        script.onload = () => {
          callback();
        };
      }
    },

    payWithBasqet() {
      this.scriptLoaded &&
        this.scriptLoaded.then(() => {
          const basqetOptions = {
            amount: this.amount,
            currency: this.currency,
            ref: this.reference,
            email: this.email,
            public_key: this.publicKey,
            description: this.description,
            onSuccess: (reference) => {
              this.onSuccess(reference);
            },
            onError: (error) => {
              this.onError(error)
            },
            onClose: () => {
              this.onClose();
            }
          };

          window.payWithBasqet(basqetOptions);
        });
    },
  },
};
</script>