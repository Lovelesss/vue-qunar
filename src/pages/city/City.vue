<template>
    <div>
        <city-header></city-header>
        <city-search :cities="cities"></city-search>
        <city-list :hotCities="hotCities" :cities="cities" :letter="letter"></city-list>
        <city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
    </div>
</template>

<script>
    import axios from 'axios'
    import CityHeader from './components/Header'
    import CitySearch from './components/Search'
    import CityList from './components/List'
    import CityAlphabet from './components/Alphabet'
    import {mapState} from 'vuex'

    export default {
        name: "City",
        components: {
            CityHeader,
            CitySearch,
            CityList,
            CityAlphabet,
        },
        data() {
            return {
                hotCities: [],
                cities: {},
                letter: '',
                lastCity: ''
            }
        },
        computed: {
            ...mapState({
                city: 'city'
            })
        },
        mounted() {
            this.$nextTick(() => {
                this.lastCity = this.city;
                this.getCityInfo();
            })
        },
        activated() {
            if(this.lastCity !== this.city) {
                this.lastCity = this.city;
                this.getCityInfo();
            }
        },
        methods: {
            getCityInfo() {
                axios.get(`/api/city.json?city=${this.city}`).then(this.getCityInfoSuccess)
            },
            getCityInfoSuccess(res) {
                if(res.data.status ===0) {
                    const data = res.data.data;
                    this.hotCities = data.hotCities;
                    this.cities = data.cities;
                }
            },
            //处理接受的字母
            handleLetterChange(letter) {
                this.letter = letter;
            }
        }
    }
</script>

<style lang="stylus" scoped>
    @import "~style/varibles.styl"
</style>