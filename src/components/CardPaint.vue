<template>
    <div class="item-card-paint">
        <div v-for="item in items" v-bind:style="(item.salary === 'None') ? 'opacity: 0.50;': 'opacity: 1;'" class="Card" v-on:click="sendItem(item)">
            <img :src="item.itemMainImg" alt="" />
            <div class="Card-wrapper">
                <div class="description">
                    <h2>{{item.name}}</h2>
                    <h2>{{item.author}}</h2>
                </div>
                <div class="saled" v-if="(item.salary === 'None')">
                    <h3>Продана на аукционе</h3>
                </div>
                <div class="salary-and-buy" v-else>
                    <div class="salary-items">
                        <h4>{{(item.oldSalary !== "None") ? item.oldSalary : ""}}</h4>
                        <h3>{{(item.salary !== "None") ? item.salary : ""}}</h3>
                    </div>
                    <div class="check-buy-item" @click.stop>
                        <button class="btn-buy" @click="custom(item.id)"
                            v-show="(item.salary !== 'None') ? true : false" v-if="(item.check === 1)">Купить</button>
                        <button class="btn-buy" style="background-color: #C1B4B1;" @click="custom(item.id)"
                            v-show="(item.salary !== 'None') ? true : false"
                            v-else-if="(item.check === 2)">Обработка</button>
                        <button class="btn-buy btn-korzina" @click="custom(item.id)"
                            v-show="(item.salary !== 'None') ? true : false" v-else>
                            <span> В корзине</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['items'],
    
    data() {
        return {

        }
    },
    methods: {
        custom(getId) {
            const check = this.items[getId - 1].check
            this.items[getId - 1].check = 2
            setTimeout(() => {
                (check === 1) ? this.items[getId - 1].check = 3 : this.items[getId - 1].check = 1
                this.$emit('custom', this.items)
            }, 2000)
            
        },
        sendItem(item){
            this.$emit('open', item)
        }
    }
} 
</script>

<style>
.Card {
    width: 280px;
    height: 328px;
    border: 1px solid #E1E1E1;
    display: flex;
    flex-direction: column;
}


.Card:hover {
    scale: 1.05;
    transition: 0.5s;
    cursor: pointer;
}

h2 {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 400;
    line-height: 150%;
    font-size: 18px;
}

.Card-wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;

}

.description {
    width: 100%;
    height: 80px;
    display: flex;
    flex-direction: column;
    justify-content: center;

}

.description h2 {
    margin-left: 24px;

}

.salary-and-buy {
    width: 100%;
    display: flex;
}

.item-card-paint {
    display: flex;
    justify-content: space-between;
}

.salary-items {
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

h3 {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 400;
    line-height: 150%;
    font-size: 16px;
}

h4 {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 400;
    line-height: 150%;
    font-size: 14px;
}

.check-buy-item {
    width: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.saled {
    width: 100%;
    height: 48px;
    display: flex;
    align-items: center;
}

.saled h3 {
    margin-left: 24px;
}

.salary-items h4 {
    text-decoration: line-through;
    color: #A0A0A0;
}

.btn-buy {
    width: 112px;
    height: 48px;
    background-color: #403432;
    color: white;
}

.btn-korzina {
    background-color: #5B3A32;

}

.btn-korzina span::before {
    content: "\2713";
}
</style>