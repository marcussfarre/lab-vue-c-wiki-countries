<template>
    <div class="bodyList">
        <div class="spinner-border text-secondary" role="status" v-if="!loadedContries">
            <span class="visually-hidden">Loading...</span>
        </div>
        <ul id="example-1" v-if="loadedContries">
            <li v-for="country in countries" class="country">
                <router-link :to="`/list/${country.alpha3Code}`">
                    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="">
                    <p>{{ country.name.common }}</p>
                </router-link>
            </li>
          </ul>
    </div>
</template>

<script>
    export default {
        name: 'CountriesList',
        data() {
            return {
                countries: [],
                loadedContries: false,
            }
        },
        mounted() {
            this.fetchCountries()
        },
        methods: {
            async fetchCountries() {
                const response = await fetch('https://ih-countries-api.herokuapp.com/countries');
                const data = await response.json();
                this.countries = data;
                this.loadedContries = true;
            }
        }
    }
</script>

<style>
    .bodyList {
        margin: 2% 10%;
    }
    .country {
        text-align: center;
        border: 1px solid black;
        width: 20%;
        margin-bottom: 3%;
    }
    .country:hover {
        background-color: grey;
    }
    img {
        width: 27px;
        height: 20px;
        margin-bottom: 2%;
    }
    p {
        color: black;
        list-style: none;
        text-decoration: none;
    }
    li {
        list-style: none;
    }
</style>