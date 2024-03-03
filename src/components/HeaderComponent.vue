<template>
    <header>
        <div class="container flex-between m-0">
            <img class="logo" src="../assets/logo-curved.png" alt="Logo">
            <img   @click="$emit('isShow')" class="arrow" :class="this.show ? 'active' : ''" src="../assets/arrow.svg" alt="Arrow">
        </div>
    </header>
</template>

<script>
    export default {
        props: ['show'],
        emit: ['isShow'],
       
    }
</script>

<style lang="scss" scoped>
 @use '../styles/partials/variables' as *;

header {
    padding-block: 1rem;
    
}
.logo {
    max-width: 50%;
    @media (min-width: 768px) {
        margin-inline: auto;
    }
}
.arrow {
    max-width: 20px;
    transition: $transition;
    &.active {
        transform: rotate(180deg);
    }
    @media (min-width: 768px) {
        display: none;
    }
}


</style>