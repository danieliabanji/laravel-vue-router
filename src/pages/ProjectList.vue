<template>
    <section>
        <h1 class="text-center">
            Lista dei progetti
        </h1>
        <ProjectCard></ProjectCard>

    </section>
</template>

<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
import { store } from '../store.js';

export default {
    name: "ProjectList",
    components: { ProjectCard },
    data() {
        return {
            store,
            projects: [],
            currentPage: 1,
            lastPage: null,
            total: 0,
        };
    },


}
</script>

<style lang="scss" scoped>

</style>