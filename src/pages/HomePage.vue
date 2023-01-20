<template>
    <section>
        <div class="row1-container">
            <div class="box box-down cyan">
                <h2>Chi Siamo</h2>
                <p>Monitors activity to identify project roadblocks</p>
                <router-link :to="{ name: 'about' }" active-class="active" class="my_btn ">
                    Explore
                </router-link>
                <img src="https://assets.codepen.io/2301174/icon-supervisor.svg" alt="">
            </div>

            <div class="box red">
                <h2>Progetti</h2>
                <p>Scans our talent network to create the optimal team for your project</p>
                <router-link :to="{ name: 'projects' }" active-class="active" class="my_btn ">
                    Explore
                </router-link>
                <img src="https://assets.codepen.io/2301174/icon-team-builder.svg" alt="">
            </div>

            <div class="box box-down blue">
                <h2>Contattaci</h2>
                <p>Uses data from past projects to provide better delivery estimates</p>
                <router-link :to="{ name: 'contact' }" active-class="active" class="my_btn ">
                    Explore
                </router-link>
                <img src="https://www.iconpacks.net/icons/1/free-mail-icon-142-thumb.png" class="mail" alt="">

            </div>
        </div>
        <div class="row2-container">
            <div class="box orange">
                <h2>Accedi</h2>
                <p>Regularly evaluates our talent to ensure quality</p>
                <a href="http://localhost:8000" class="my_btn">Explore</a>
                <img src="https://assets.codepen.io/2301174/icon-calculator.svg" alt="">

            </div>
        </div>

    </section>
</template>

<script>
export default {
    name: 'HomePage',
}
</script>

<style lang="scss" scoped>
// VARIABLES

$red: hsl(0, 78%, 62%);
$cyan: hsl(180, 62%, 55%);
$orange: hsl(34, 97%, 64%);
$blue: hsl(212, 86%, 64%);
$varyDarkBlue: hsl(234, 12%, 34%);
$grayishBlue: hsl(229, 6%, 66%);
$veryLightGray: hsl(0, 0%, 98%);
$weight1: 200;
$weight2: 400;
$weight3: 600;
$color-btn-text: #3363ff;
$color-btn-background: #e6ecff;

$transition: .2s;


body {
    // font-size: 15px;
    background-color: $veryLightGray;
}

section {
    margin-top: 7.5rem;
}

.mail {
    width: 35%;
}

.box p {
    color: $grayishBlue;
}

.box {
    border-radius: 5px;
    box-shadow: 0px 30px 40px -20px $grayishBlue;
    padding: 40px;
    margin: 30px;
}

img {
    float: right;
}

@media (max-width: 450px) {
    .box {
        height: 200px;
    }
}

@media (max-width: 950px) and (min-width: 450px) {
    .box {
        text-align: center;
        height: 180px;
    }
}

.cyan {
    border-top: 3px solid $cyan;
}

.red {
    border-top: 3px solid $red;
}

.blue {
    border-top: 3px solid $blue;
}

.orange {
    border-top: 3px solid $orange;
}

h2 {
    color: $varyDarkBlue;
    font-weight: $weight3;
}


@media (min-width: 950px) {
    .row1-container {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .row2-container {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .box-down {
        position: relative;
        top: 150px;
    }

    .box {
        width: 20%;

    }

    .header p {
        width: 30%;
    }

}

.my_btn {
    display: block;
    width: 60%;
    padding: .5rem;
    font-size: 1rem;
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
</style>