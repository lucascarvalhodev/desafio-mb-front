<script>
    export default {
        name: 'ButtonCustom',
        props: ['outline'],
    }
</script>

<template>
    <button class="button" :class="{'button-outline': outline}"><slot /></button>
</template>
