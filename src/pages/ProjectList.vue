<template>
    <section>
        <h1 class="text-center">
            Lista dei progetti
        </h1>
        <div class="row mt-5">
            <div class="col-12 col-md-4" v-for="(project, index) in projects" :key="index">
                <div class="card" style="width: 18rem;">
                    <img :src="`${store.imageBasePath}${project.cover_image}`" class="card-img-top"
                        :alt="project.title">
                    <div class="card-body">
                        <h5 class="card-title">
                            {{ project.title }}
                        </h5>
                        <p class="card-text">
                            {{ truncateContent(project.content ) }}
                        </p>
                        <router-link class="btn btn-primary"
                            :to="{ name: 'single-project', params: { slug: project.slug } }">
                            Vedi il post
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
        <div class="">
            <nav aria-label="Page navigation example">
                <ul class="pagination">
                    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
                    <li class="page-item" v-for="(n, index) in lastPage" :key="index">
                        <a class="page-link" @click="getProjects(n)"> {{ n }}</a>
                    </li>
                    <li class="page-item"><a class="page-link" href="#">Next</a></li>
                </ul>
            </nav>
        </div>
    </section>
</template>

<script>
import axios from 'axios';
import { store } from '../store.js';

export default {
    name: 'ProjectList',
    data() {
        return {
            store,
            projects: [],
            currentPage: 1,
            lastPage: null,
            total: 0,
            contentMaxLen: 100,
        }
    },
    methods: {
        getProjects(pagenum) {
            axios.get(`${this.store.apiBaseUrl}/projects`, {
                params: {
                    page: pagenum
                }
            }).then((response) => {
                // console.log(response.data.results);
                this.projects = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.total = response.data.results.total;

            })
        },
        truncateContent(text) {
            if (text.length > this.contentMaxLen) {
                return text.substr(0, this.contentMaxLen) + '...';
            }
            return text;
        }
    },
    mounted() {
        this.getProjects(1);
    }
}
</script>

<style lang="scss" scoped>

</style>