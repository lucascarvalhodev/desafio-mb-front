<script>
  import FormStep1 from '../FormStep1.vue'
  import FormStep2PF from '../FormStep2PF.vue'
  import FormStep2PJ from '../FormStep2PJ.vue'
  import FormStep3 from '../FormStep3.vue'
  import FormStep4 from '../FormStep4.vue'

  export default {
      name: 'RegisterForm',
      components: {
        FormStep1,
        FormStep2PF,
        FormStep2PJ,
        FormStep3,
        FormStep4,
      },
      data() {
        return {
          currentStep: 1,
          maxStep: 4,
          data: {}
        }
      },
      methods: {
        onNext(data = {}) {
          this.data = {
            ...this.data,
            ...data
          }
          if(this.currentStep < this.maxStep) {
            this.currentStep = this.currentStep + 1
          } else {
            this.onComplete()
          }
        },
        onBack() {
          if(this.currentStep > 1)
            this.currentStep = this.currentStep - 1
        },
        onComplete() {
          console.log(this.data)
        }
      }
  }
</script>

<template>
  <div>
    <div class="step-info">Etapa <span class="text-orange">{{ currentStep }}</span> de 4</div>
    <FormStep1 v-if="currentStep === 1" :onNext="onNext" :initialState="data" />
    <FormStep2PF v-if="currentStep === 2 && data.person === 'PF'" :onNext="onNext" :onBack="onBack" :initialState="data" />
    <FormStep2PJ v-if="currentStep === 2 && data.person === 'PJ'" :onNext="onNext" :onBack="onBack" :initialState="data" />
    <FormStep3 v-if="currentStep === 3" :onNext="onNext" :onBack="onBack" :initialState="data" />
    <FormStep4 v-if="currentStep === 4" :onNext="onNext" :onBack="onBack" :initialState="data" />
  </div>
</template>

