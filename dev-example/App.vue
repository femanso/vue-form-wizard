<template>
  <div>
    <form-wizard @on-complete="onComplete"
                 shape="circle"
                 color="#000000"
                 @on-loading="setLoading"
                 class="card">
      <tab-content title="Personal details"
                   :before-change="validateAsync"
                   route="/first"
                   icon="ti-user">
      </tab-content>
      <tab-content title="Additional Info"
                   :before-change="validate"
                   route="/second"
                   icon="ti-settings">
      </tab-content>
      <tab-content title="Last step"
                   :before-change="validateAsync"
                   route="/third"
                   icon="ti-check">
      </tab-content>
      <transition name="fade" mode="out-in">
        <router-view></router-view>
      </transition>
      <div class="loader" v-if="loadingWizard"></div>
    </form-wizard>
  </div>
</template>

<script>

  export default {
    name: 'app',
    data () {
      return {
        loadingWizard: false
      }
    },
    methods: {
      onComplete () {
        alert('Yay!')
      },
      setLoading (value) {
        this.loadingWizard = value
      },
      validateAsync () {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            var firstcb = document.getElementById("firstcb");
            if(firstcb.checked) {
              resolve(true)
            } else {
              reject('checkbox is required')
            }
          }, 1000)
        })
      },
      validate () {
        return true
      }
    }
  }
</script>
<style>
  @import "loader.css";
</style>
<style lang="scss">
  $border-radius-extreme: 6px !default;
  $white-color: white;
  $gray-input-bg: #F3F2EE !default;
  $card-black-color: #252422 !default;

  body {
    margin-top: 20px;
    background-color: #ecf0f1;
  }

  .card-footer {
    padding: 0px 20px;
  }

  .card {
    border-radius: $border-radius-extreme;
    box-shadow: 0 2px 2px rgba(204, 197, 185, 0.5);
    background-color: $white-color;
    color: $card-black-color;
    padding: 10px 0;
    margin-bottom: 20px;
    position: relative;
    z-index: 1;
  }

</style>
