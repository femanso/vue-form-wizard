<template>
  <div v-if="active" class="tab-container">
    <div v-if="validationError">
     {{ validationError }}
    </div>
    <slot>
    </slot>
  </div>
</template>
<script>
  export default{
    name: 'tab-content',
    props: {
      title: {
        type: String,
        default: ''
      },
      /***
       * Icon name for the upper circle corresponding to the tab
       * Supports themify icons only for now.
       */
      icon: {
        type: String,
        default: ''
      },
      /***
       * Function to execute before tab switch. Return value must be boolean
       * If the return result is false, tab switch is restricted
       */
      beforeChange: {
        type: Function
      },
      route: {
        type: [String, Object]
      }
    },
    data () {
      return {
        active: false,
        validationError: null
      }
    }
  }
</script>
