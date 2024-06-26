<script setup>
    import { ref } from "vue";
    const Datadetail = ref([])

    const apiHandler = async () => {
        try {
            const response = await fetch(
                'https://min-api.cryptocompare.com/data/top/totalvolfull?limit=10&tsym=USD')
            const data = await response.json()
            console.log(data.Data);
            Datadetail.value = data.Data
        } catch (error) {
            console.log(error);
        }
    }

    apiHandler()
</script>

<template>
    <div class="detailBox">
        <div class="Datatitle">
            <h1 class="title">幣別</h1>
            <h1 class="title">價格</h1>
            <h1 class="title">24h漲跌幅</h1>
        </div>
        <div v-for="item in Datadetail" :key="item.id">
            <router-link class="detail" :to="{name:'detail',params: { id: item.RAW.USD.FROMSYMBOL }}">
                <div class="detailInfo picArea">
                    <div class="CoinPic" :style="{backgroundImage: `url(${item.RAW.USD.IMAGEURL})`}">
                    </div>
                    <div class="right">
                        <div class="CoinName">{{ item.CoinInfo.Name }}</div>
                        <div class="CoinVolue">{{ item.RAW.USD.VOLUME24HOUR }}</div>
                    </div>
                </div>
                <div class="detailInfo priceArea">
                    <div class="CoinPrice">{{ item.RAW.USD.PRICE }}</div>
                </div>
                <div class="detailInfo changeArea">
                    {{ item.DISPLAY.USD.CHANGEPCT24HOUR }}%
                </div>
            </router-link>
        </div>
    </div>
</template>

<style>
    .detailBox {
        width: 100%;
        min-height: 100vh;
    }

    .Datatitle{
        width: 100%;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        border: 1px solid #fff;
    }

    .Datatitle h1.title{
        flex: 1;
        color: #fff;
        font-size: 1.1rem;
        border-right: 1px solid #fff;
        padding: 1%;
        text-align: center;
    }

    .Datatitle h1.title:first-child{
        flex: 2;
    }

    .Datatitle h1.title:last-child{
        border-right: 0px;
    }

    .detailBox .detail {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        padding: 2%;
        border-bottom: 1px solid rgb(223, 223, 223);
        text-decoration: none;
    }

    .detailBox .detail .detailInfo {
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 1;
        color: #fff;
        text-align: center;
    }

    .detailBox .detail .picArea{
        flex: 2;
        justify-content: flex-start;
    }

    .CoinPic{
        width: 30%;
        padding-top: 40%;
        background-repeat: no-repeat;
        background-size: contain;
        background-position: center;
        margin-right: 10%;
    }

    .right{
        text-align: left;
    }
</style>