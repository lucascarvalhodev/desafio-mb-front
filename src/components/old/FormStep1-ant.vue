<script>
    import ButtonCustom from '../ButtonCustom.vue'
    import InputCustom from '../InputCustom.vue'
    import { object, string } from 'yup';

    export default {
      name: 'FormStep1',
      components: {
        InputCustom,
        ButtonCustom
      },
      props: {
        onNext: Function,
      },
      data() {
        return {
          email: undefined,
          person: undefined,
          errors: []
        }
      },
      methods: {
        async next() {
          let schema = object({
            email: string().email().required(),
            person: string().required(),
          });

          try {
            const data = await schema.validate({
              email: this.email,
              person: this.person
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
    <div class="title">Seja bem vindo(a)</div>
    <div class="mb-10">
      <InputCustom label="Endereço de e-mail" v-model="email" />
      <div class="flex gap-10">
        <input type="radio" id="one" value="PF" v-model="person" />
        <label class="label" for="one">Pessoa física</label>
        <input type="radio" id="two" value="PJ" v-model="person" />
        <label class="label" for="two">Pessoa jurídica</label>
      </div>
    </div>
    <div class="box-errors mb-10" v-if="errors.length > 0">
      <div v-for="error in errors" :key="error">{{error}}</div>
    </div>
    <div class="flex gap-10">
      <ButtonCustom @click="next">Continuar</ButtonCustom>
    </div>
  </div>
</template>


