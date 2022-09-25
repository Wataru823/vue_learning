<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs, onMounted, onBeforeMount, onUpdated } from 'vue'

// const itemName1 = ref<string>('Desk')
const itemName2 = 'Bike'

const item1 = reactive({
    name: 'Desk',
    price: 40000
})

// const price1 = 40000
const price2 = 20000

const url1 = 'https://www.amazon.co.jp/IT%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%80%8C%E4%BA%BA%E7%94%9F%E6%88%A6%E7%95%A5%E3%80%8D%E3%81%AE%E6%95%99%E7%A7%91%E6%9B%B8-%E6%8A%80%E8%A1%93%E3%82%92%E6%AD%A6%E5%99%A8%E3%81%AB%E3%80%81%E5%85%85%E5%AE%9F%E3%81%97%E3%81%9F%E4%BA%BA%E7%94%9F%E3%82%92%E9%80%81%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AE%E3%80%8C%E3%83%93%E3%82%B8%E3%83%8D%E3%82%B9%E3%80%8D%E3%81%A8%E3%80%8C%E3%83%9E%E3%82%A4%E3%83%B3%E3%83%89%E3%82%BB%E3%83%83%E3%83%88%E3%80%8D%EF%BC%88%E5%9B%BA%E5%AE%9A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E7%89%88%EF%BC%89-%E5%B9%B3%E5%9F%8E-%E5%AF%BF-ebook/dp/B06W5VDHPW/ref=sr_1_2?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&keywords=%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2+%E7%8B%AC%E7%AB%8B&qid=1660640689&s=digital-text&sr=1-2'

const buy = (itemName: string) => {
    alert('Are you sure to buy ' + itemName + '?')
}

const clear = (event: any) => {
    item1.name = ''
    item1.price = 0
}

const budget = 50000

// const priceLabel = computed(() => {
//     if (item1.price > budget * 2) {
//         return 'tooooo expensive..'
//     } else if (item1.price > budget) {
//         return 'expensive..'
//     } else {
//         return item1.price + ' yen'
//     }
// })

onBeforeMount(() => {
    console.log('before mount')
})

onMounted(() => {
    console.log('mounted')
})

onUpdated(() => {
    console.log('update')
})

const priceLabel = ref<string>(item1.price + ' yen')
const { price } = toRefs(item1)
watch(price, () => {
    if (price.value > budget * 2) {
        priceLabel.value = 'tooooo expensive..'
    } else if (price.value > budget) {
        priceLabel.value = 'expensive..'
    } else {
        priceLabel.value = price.value + ' yen'
    }
})

</script>

<template>
    <div class="container">
        <h1>Payment</h1>
        <input v-model="item1.name" />
        <input v-model="item1.price" />
        <button @click="clear">Clear</button>

        <div class="payment">
            <label>{{ item1.name }}</label>
            <label>{{ priceLabel }}</label>
            <!-- <label>{{ item1.price }} 円</label> -->
            <a :href="url1">bought at...</a>
            <button @click="buy(item1.name)">BUY</button>
        </div>
        <div class="payment">
            <label>{{ itemName2 }}</label>
            <label>{{ price2 }} yen</label>
            <button @click="buy(itemName2)">BUY</button>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.payment {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    width: 400px;
    background-color: aliceblue;
    margin-bottom: 8px;
}

input {
    margin-bottom: 8px;
}

label {
    font-style: 20px;
}
</style>