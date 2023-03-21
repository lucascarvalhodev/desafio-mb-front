<script>
    import ButtonCustom from '../ButtonCustom.vue'
    import InputCustom from '../InputCustom.vue'
    import { object, string } from 'yup'

    export default {
      name: 'FormStep3',
      components: {
        InputCustom,
        ButtonCustom
      },
      props: {
        onNext: Function,
        onBack: Function,
      },
      data() {
        return {
          password: '',
          errors: []
        }
      },
      methods: {
        async next() {
        let schema = object({
          password: string().required(),
        });

        try {
          const data = await schema.validate({
          password: this.password,
        }, {abortEarly: false})
          this.onNext(data)
        } catch(e) {
          this.errors = e.errors
        }
      }
    }
  }
</script>

<template>
  <div>
    <div class="title">Senha de acesso</div>
    <div class="mb-10">
      <InputCustom type="password" label="Sua senha" v-model="password" />
    </div>
    <div class="box-errors mb-10" v-if="errors.length > 0">
      <div v-for="error in errors" :key="error">{{error}}</div>
    </div>
    <div class="flex gap-10">
      <ButtonCustom outline="true" @click="onBack">Voltar</ButtonCustom>
      <ButtonCustom @click="next">Continuar</ButtonCustom>
    </div>
  </div>
</template>


