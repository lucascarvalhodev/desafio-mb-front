<script>
    import ButtonCustom from '../ButtonCustom.vue'
    import InputCustom from '../InputCustom.vue'
    import { object, string, date } from 'yup'

    export default {
      name: 'FormStep2PF',
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
          name: undefined,
          document: undefined,
          birthDate: undefined,
          phoneNumber: undefined,
          errors: []
        }
      },
      methods: {
        async next() {
          let schema = object({
            name: string().required(),
            document: string().required(),
            birthDate: date().required(),
            phoneNumber: string().required()
          });

          try {
            const data = await schema.validate({
            name: this.name,
            document: this.document,
            birthDate: this.birthDate,
            phoneNumber: this.phoneNumber
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
    <div class="title">Pessoa Física</div>
    <div class="mb-10">
      <InputCustom label="Nome" v-model="name" />
      <InputCustom label="CPF" v-model="document" />
      <InputCustom type="date" label="Data de nascimento" v-model="birthDate" />
      <InputCustom label="Telefone" v-model="phoneNumber" />
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
