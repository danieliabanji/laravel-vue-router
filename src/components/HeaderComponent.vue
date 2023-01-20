<template>
    <header>
        <nav class="navebar  bg-dark navbar-expand-lg">
            <div class="container-fluid d-flex">
                <a class="navbar-brand col-md-3 fs-4 col-lg-2 me-0 px-3 logo" href="/">BoolPress</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                    aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">

                        <li class="nav-item " v-for="(item, index) in menuItems" :key="index">
                            <router-link :to="{ name: item.routeName }" active-class="active" class="nav-link ">
                                {{ item.label }}
                            </router-link>
                        </li>
                        <li class="nav-item">
                            <a href="http://localhost:8000" target="_blank" class="nav-link te">Accedi</a>
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
                    label: 'Progetti',
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
.navebar {
    width: 100%;
    margin: auto;
    padding: 35px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.logo {
    /*   cursor: pointer; */
    /*   background-color: #FFEA11; */
    color: #FFEA11;
    margin-left: 5px;
}

.navebar ul li {
    list-style: none;
    display: inline-block;
    margin: 0 20px;
    /*padding: 0 20px; */
    position: relative;

}

.navebar ul li a {
    text-decoration: none;
    color: #FFEA11;
    text-transform: capitalize;
}

.navebar ul li::after {
    content: '';
    height: 2px;
    width: 0;
    /*100% */
    background: #009688;
    position: absolute;
    left: 0;
    bottom: -8px;
    transition: 0.5s;
}

.navebar ul li:hover::after {
    width: 100%;
}
</style>