<template>
    <router-view>
        <div v-if="showCountry">
            <div class="container text-center">
                <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="" class="imgDetails">
                <h3>{{ country.name.common }}</h3>
                <div class="row align-items-start">
                    <div class="col">
                        <p>Capital</p>
                    </div>
                    <div class="col">
                        <p v-for="cap in country.capital"> {{ cap }} </p>
                    </div>
                    <hr>
                </div>
                <div class="row align-items-start">
                    <div class="col">
                        <p>Area</p>
                    </div>
                    <div class="col">
                        <p>{{ country.area }} km^2</p>
                    </div>
                    <hr>
                </div>
                <div class="row align-items-start">
                    <div class="col">
                        <p>Borders</p>
                    </div>
                    <div class="col">
                        <router-link :to="`/list/${border}`" v-for="border in country.borders">
                            {{ border }} 
                            <br>
                        </router-link>
                    </div>
                </div>
              </div>
        </div>
    </router-view>
</template>

<script>
    export default {
        name: 'CountryDetails',
        data() {
            return {
                countryCode: '',
                country: Object,
                showCountry: false,
            }
        },
        created() {
            const { alpha3Code } = this.$route.params;
            this.countryCode = alpha3Code;
            this.$watch( () => this.$route.params, (toParams) => {
                const { alpha3Code } = toParams;
                this.countryCode = alpha3Code;
                this.getCountryByCode();
                }
            );
        },
        methods: {
            async getCountryByCode() {
                if (this.countryCode) {
                    const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${this.countryCode}`);
                    const data = await response.json();
                    this.country = data;
                    this.showCountry = true;
                } else {
                    this.showCountry = false;
                }
            },
            async getNameByCountryCode(countryCode) {
                const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${countryCode}`);
                const data = await response.json();
                console.log(data.name.common);
                return data.name.common;
            }
        }
    }
</script>

<style>
.imgDetails {
    width: 70%;
    height: 50%;
}
</style>