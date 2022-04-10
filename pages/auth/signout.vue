<template>
<h1>Sign Out</h1>
</template>

<script>
export default {
async AsyncData(){
    $nuxt.$fire.$auth.signOut()
}
}
</script>

<style>

</style>