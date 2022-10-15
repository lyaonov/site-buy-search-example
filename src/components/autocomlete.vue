<template>
    <div class="autocomplete">
        <div class="popover">
            <input type="text" v-model="query" placeholder="Поиск">
            <button class="btn-search">Найти</button>
            <div class="options" v-show="visible">
                <ul>
                    <li v-for="( match,index ) in matches" :key="match[filterby]"
                        :class="{'selected': (selected == index)}" @click="itemClicked(index)" v-text="match[filterby]">
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['items', 'filterby'],
    data() {
        return {
            selectedItem: null,
            query: '',
            visible: false,
            selected: 0,
        }
    },
    methods: {
        toggleVisible() {
            this.visible = !this.visible
        },
        itemClicked(index) {
            this.selected = index;
            this.selectItem();
        },
        selectItem() {
            this.selectedItem = this.matches[this.selected]
            this.visible = false
            this.query = ''
        }

    },
    computed: {
        matches() {
            if (this.query == '') {
                this.visible = false
                return []
            }
            this.visible = true

            return this.items.filter((item) => item[this.filterby].toLowerCase().includes(this.query.toLowerCase()))
        }
    }
}
</script>

<style scoped>
.autocomplete {
    position: relative;
    width: 416px;
}

.input {
    height: 40px;
    width: 294px;
    border-radius: 3px;
    border: 2xp solid lightblue;
    box-shadow: 0 0 10px lightgray;
    font-size: 25px;
    padding-left: 10px;
    padding-top: 10px;
    cursor: text;
}



.btn-search {
    margin-top: 5px;
    width: 122px;
    height: 48px;
    background-color: #403432;
    color: white;
}

.btn-search:hover {
    background-color: #776763;
    color: white;
}

.popover {
    width: 100%;
    min-height: 59px;
    position: relative;
    background: #F6F3F3;
    border-radius: 3px;
    text-align: center;
    display: flex;
}

.popover input {
    width: 285px;
    margin-top: 5px;
    height: 46px;
    font-size: 16px;
    border: 1px solid lightgray;
    padding-left: 8px;
}

.options {
    position: absolute;
    width: 100%;
    top: 59px;
    max-height: 150px;
    overflow-y: scroll;
    margin-top: 5px;
    z-index: 2;
}

.options ul {
    margin: 0;
    background: #f1f1f1;
    list-style-type: none;
    text-align: left;
    padding-left: 0;
}

.options ul li {
    border-bottom: 1px solid lightgray;
    padding: 10px;
    cursor: pointer;
    background: #f1f1f1;
}

.options ul li:hover {
    background: #776763;
    color: #fff;
    font-weight: 600;
}
</style>