<template>
    <section>
        <h1 class="text-center">About Us</h1>
        <p>Questo è un sito dove sono raccolti i miei progetti.</p>
        <p>progetti svolti:
            <router-link :to="{ name: 'projects' }">
                progetti
            </router-link>
        </p>
    </section>
</template>

<script>
export default {
    name: 'AboutUs',
}
</script>

<style lang="scss" scoped>

</style>