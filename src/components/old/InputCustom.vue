<script>
    export default {
        name: 'InputCustom',
        props: {
            label: String,
            name: String,
            type: String,
            modelValue: String,
            value: String
        },
        methods: {
            updateValue(event) {
                this.$emit('update:modelValue', event.target.value);
            }
        },
    }
</script>

<template>
    <div class="input-box">
      <label class="label" :for="name" v-if="label">{{ label }}</label>
      <input class="input" :type="type" :name="name" :value="modelValue" @input="updateValue" />
    </div>
</template>
