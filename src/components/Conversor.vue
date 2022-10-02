<template>
    <div class="conversor">
        <h2>{{moedaA}} Para {{moedaB}}</h2>
        <input type="text" v-model="moedaA_value" :placeholder="moedaA">
        <input type="button" value="Converter" @click="converter">
        <h2>{{moedaB_value}}</h2>
    </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Conversor',
    props: ['moedaA', 'moedaB'],
        data(){
            return{
                moedaA_value: "",
                moedaB_value: 0
            }
        },
        methods:{

            converter(){
                let de_para= this.moedaA + "_" + this.moedaB

                let url = `https://api.invertexto.com/v1/currency/${de_para}?token=1664|3HaSJDM9q8Nvtr2BOumsuMIq7WogGqr1`

                fetch(url).then(res => {
                    return res.json()
                })
                .then(json => {
                let transformObjToArr = Object.keys(json).map(arr => {
                    return [json[arr]]
                })
                let cotacao = transformObjToArr[0][0].price
                this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2)
                })
            }
        }
}
</script>

<style scoped>
    .conversor{
        padding: 20px;
        max-width: 300px;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    }
</style>