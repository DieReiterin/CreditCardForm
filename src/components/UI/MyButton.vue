<template>
    <button :class="{
        'button_github': buttonType === 'github', 
        'button_regular': buttonType === 'regular', }"
    :disabled="buttonType === 'regular'"
    ><slot></slot></button>
</template>
<script>
export default {
    name: 'my-button',
    props: {
        buttonType: {
            type: String,
            required: false,
            default: 'regular',
        }
    }
}
</script>
<style scoped>
.button_regular {
    width: 100%;
    height: 55px;
    color: #fff;
    font-size: 22px;
    font-weight: 500;
    border: none;
    border-radius: 5px;
    box-shadow: 3px 10px 20px 0px rgba(35, 100, 210, 0.3);
    background-color: var(--secondary_color);
    cursor: pointer;
}
.button_github {
    position: absolute;
    left: 150%;    
    top: 40%;
    width: 170px;
    height: 55px;
    color: #fff;
    font-size: 18px;
    font-weight: 700;
    border: none;
    border-radius: 5px;
    box-shadow: 3px 10px 20px 0px rgba(35, 100, 210, 0.3);
    background-color: #24292e;
    cursor: pointer;
}
</style>