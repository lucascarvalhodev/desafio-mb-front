<script>
    import ButtonCustom from '../ButtonCustom.vue'
    import InputCustom from '../InputCustom.vue'
    import { object, string, date } from 'yup'

    export default {
      name: 'FormStep2PJ',
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
          corporateName: undefined,
          document: undefined,
          openingDate: undefined,
          phoneNumber: undefined,
          errors: []
        }
      },
      methods: {
        async next() {
          let schema = object({
            corporateName: string().required(),
            document: string().required(),
            openingDate: date().required(),
            phoneNumber: string().required(),
          });

          try {
            const data = await schema.validate({
            corporateName: this.corporateName,
            document: this.document,
            openingDate: this.openingDate,
            phoneNumber: this.phoneNumber,
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
    <div class="title">Pessoa Jurídica</div>
    <div class="mb-10">
      <InputCustom label="Razão social" v-model="corporateName" />
      <InputCustom label="CNPJ" v-model="document" />
      <InputCustom type="date" label="Data de abertura" v-model="openingDate" />
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


