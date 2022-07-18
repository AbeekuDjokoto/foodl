<template>
  <button>{{ text }}</button>
</template>

<script>
export default {
    props: {
        text: {
            type: String
        }
    }
}
</script>

<style scoped>
button{
    padding: 21px 61px;
    font-family: 'IBM Plex Sans';
    font-style: normal;
    font-weight: 500;
    font-size: 24px;
    line-height: 130%;
    /* or 31px */
    letter-spacing: -0.04em;
    text-align: center;
    color: #FFFFFF;
    background: #000000;
    box-shadow: 0px 16px 40px rgba(192, 86, 10, 0.4);
    border-radius: 8px;
}

</style>