<template>
    <header>
        <nav class="navbar  bg-dark navbar-expand-lg">
            <div class="container-fluid ">
                <a class="navbar-brand col-md-3 col-lg-2 me-0 px-3 text-white" href="/">BoolPress</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                    aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">

                        <li class="nav-item " v-for="(item, index) in menuItems" :key="index">
                            <router-link :to="{ name: item.routeName }" active-class="active"
                                class="nav-link text-white">
                                {{ item.label }}
                            </router-link>
                        </li>


                    </ul>

                </div>
            </div>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'HeaderComponent',
    data() {
        return {
            menuItems: [
                {
                    label: 'Home',
                    routeName: 'home'
                },
                {
                    label: 'Projects',
                    routeName: 'projects'
                },
                {
                    label: 'Chi siamo',
                    routeName: 'about'
                },
                {
                    label: 'Contatti',
                    routeName: 'contact'
                },

            ]
        }
    }
}
</script>

<style lang="scss" scoped>

</style>