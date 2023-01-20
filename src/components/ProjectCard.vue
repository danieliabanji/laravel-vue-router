<template>

    <div class="row g-4 mt-5">
        <div class="col-12 col-md-4" v-for="(project, index) in projects" :key="index">
            <div class="grid">
                <div class="grid__item">
                    <div class="mycard">
                        <img class="mycard__img" :src="`${store.imageBasePath}${project.cover_image}`"
                            :alt="project.title">
                        <div class="mycard__content">
                            <h2 class="mycard__header">{{ project.title }}</h2>
                            <p class="mycard__text"> {{ truncateContent(project.content ) }}</p>
                            <router-link class="mycard__btn"
                                :to="{ name: 'single-project', params: { slug: project.slug } }">
                                Vedi il post <span>&rarr;</span>
                            </router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>





    <div class="d-flex flex-row-reverse mt-5">
        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item"><a class="page-link" @click="prev()">Previous</a></li>
                <li class="page-item" v-for="(n, index) in lastPage" :key="index">
                    <a class="page-link" @click="getProjects(n)"> {{ n }}</a>
                </li>
                <li class="page-item"><a class="page-link" @click="next()">Next</a></li>
            </ul>
        </nav>
    </div>
</template>

<script>
import axios from 'axios';
import { store } from '../store.js';
export default {
    name: 'ProjectCard',
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
        },
        prev() {
            this.currentPage--;
            if (this.currentPage < 1) {
                this.currentPage = this.currentPage;
            }
            axios.get(`${this.store.apiBaseUrl}/projects`, {
                params: {
                    page: this.currentPage
                }
            }).then((response) => {
                console.log(response.data.results);
                this.projects = response.data.results.data;
                // this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.total = response.data.results.total;
            })
        },
        next() {
            this.currentPage++;
            if (this.currentPage > this.lastPage) {
                this.currentPage = this.lastPage;
            }
            axios.get(`${this.store.apiBaseUrl}/projects`, {
                params: {
                    page: this.currentPage
                }
            }).then((response) => {
                console.log(response.data.results);
                this.projects = response.data.results.data;
                // this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.total = response.data.results.total;
            })
        }
    },
    mounted() {
        this.getProjects(1);
    }
}
</script>

<style lang="scss" scoped>
// MEDIA QUERY
@mixin media($breakpoint) {
    @if $breakpoint ==small {
        @media (max-width: 60em) {
            @content;
        }
    }
}

// VARIABLES
$color-header: #0d0d0d;
$color-text: #404040;

$color-btn-text: #3363ff;
$color-btn-background: #e6ecff;

$transition: .2s;

// RESET
*,
*::before,
*::after {
    margin: 0;
    padding: 0;
    box-sizing: inherit;
}

// GLOBAL
html {
    box-sizing: border-box;
    font-size: 62.5%; // 10px/16px
}

body {
    display: flex;
    justify-content: center;
    align-content: center;
    padding: 6rem;
    background-color: #f5f5f5;
    font-family: "Inter", sans-serif;

    @include media(small) {
        padding: 3rem;
    }
}

// MAIN CONTENT
.grid {
    display: grid;
    // width: 114rem;
    // grid-gap: 6rem;
    // grid-template-columns: repeat(auto-fit,
    //         minmax(30rem, 1fr));
    align-items: start;

    @include media(small) {
        grid-gap: 3rem;
    }

    &__item {
        background-color: #fff;
        border-radius: .4rem;
        overflow: hidden;
        box-shadow: 0 3rem 6rem rgba(0, 0, 0, .1);
        cursor: pointer;
        transition: $transition;

        &:hover {
            transform: translateY(-.5%);
            box-shadow: 0 4rem 8rem rgba(0, 0, 0, .2);
        }
    }
}

.mycard {
    &__img {
        display: block;
        width: 100%;
        height: 18rem;
        object-fit: cover;
    }

    &__content {
        padding: 3rem 2rem;
    }

    &__header {
        // font-size: 3rem;
        font-weight: 500;
        color: $color-header;
        margin-bottom: 1.5rem;
    }

    &__text {
        // font-size: 1.5rem;
        letter-spacing: .1rem;
        line-height: 1.7;
        color: darken($color-text, 1%);
        margin-bottom: 2.5rem;
    }

    &__btn {
        display: block;
        width: 100%;
        padding: .75rem;
        font-size: 1.25rem;
        text-align: center;
        color: $color-btn-text;
        background-color: $color-btn-background;
        border: none;
        border-radius: .4rem;
        transition: $transition;
        text-decoration: none;
        cursor: pointer;

        span {
            margin-left: 1rem;
            font-size: 1.5rem;
            transition: $transition;
        }

        &:hover,
        &:active {
            background-color: darken($color-btn-background, 2%);

            span {
                margin-left: 1.5rem;
            }
        }
    }
}
</style>