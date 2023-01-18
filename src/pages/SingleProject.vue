<template>
    <section v-if="project">
        <h1 class="text-center">
            {{ project.title }}
        </h1>
        <div class="text-center">
            <img :src="`${store.imageBasePath}${project.cover_image}`" :alt="project.title">
        </div>
        <div>
            <p>
                {{ project.content }}
            </p>
        </div>
        <!-- <div v-if="project.git_link"> -->
        <h5>
            <a :href="project.git_link"> {{ project.git_link }}</a>

        </h5>
        <!-- </div> -->
        <div v-if="project.type">
            <h5>
                Type: {{ project.type.name }}
            </h5>
        </div>
        <div v-if="project.tags && project.tags.length > 0">
            <h5>
                Tags
            </h5>
            <div>
                <span v-for="(tag, index) in project.tags" :key="index" class="badge text-bg-info m-2">
                    {{ tag.name }}
                </span>
            </div>
        </div>

    </section>
    <section v-else>
        Loading...
    </section>
</template>

<script>
import axios from 'axios';
import { store } from '../store.js';
export default {
    name: 'SingleProject',
    data() {
        return {
            store,
            project: null,
        }
    },
    methods: {
        getProject() {
            console.log(this.$route);
            axios.get(`${this.store.apiBaseUrl}/projects/${this.$route.params.slug}`).then((response) => {
                console.log(response.data.results);
                if (response.data.success) {
                    // console.log(response.data.results);
                    this.project = response.data.results;
                } else {
                    // console.log(this.$router);
                    this.$router.push({ name: 'not-found' })
                }
            })
        },

    },
    mounted() {
        this.getProject();
    }
}
</script>

<style lang="scss" scoped>
img {
    width: 100%;
    padding: 2rem 0;
}
</style>