<template>
    <div class="m-10">
        <select 
        v-model="selected" 
        @change="onChange()"
        class="form-select p-3 mt-10 block border rounded w-full ">
            <option value="0">Select Country</option>
            <option v-for="country in countries"  :value="country.ID">{{country.Country}}</option>
        </select>
    </div>
</template>

<script>
    export default {
        name:'CountrySelect',
        props: ['countries'],
        data() {
            return {
                selected: 0,
            }
        },
        methods: {
            onChange(){
                const Country = this.countries.find((country)=> country.ID === this.selected);
                
                this.$emit('get-country', Country);
            }
        },
    }
</script>