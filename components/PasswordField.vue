<template>
  <div class="icon-input right-icon">
    <i
      class="icon password-icon"
    />
    <input
      :type="passwordFieldType"
      :placeholder="$t('user.pass')"
      v-model.trim="password"
      :class="{invalid: !!!password || isInvalid}"
      @change="$emit('change', password)"
    >
    <i
      class="icon"
      :class="!isPasswordTypePassword ? 'eye-icon' : 'eye-close-icon'"
      @click="passwordFieldToggle"
    />
  </div>
</template>

<script>
  export default {
    name: 'PasswordField',
    data() {
      return {
        password: '',
        passwordFieldType: 'password'
      }
    },
    props: {
      isInvalid: {
        type: Boolean,
        default: false
      },
      value: {
        type: String
      }
    },

    watch:{
      value(value){
        this.password = value
      }
    },

    mixins: [],
    components: {},
    computed: {
      isPasswordTypePassword(){
        return this.passwordFieldType === 'password'
      },
    },
    methods: {
      passwordFieldToggle(){
        if(this.isPasswordTypePassword){
          this.passwordFieldType = 'text'
        } else {
          this.passwordFieldType = 'password'
        }
      },
    },
    mounted() {
      this.password = this.value
    }
  }
</script>

