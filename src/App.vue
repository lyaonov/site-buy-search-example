<script>
// import customers from './assets/customers'
import customers from './assets/customers';
import Autocomlete from './components/autocomlete.vue';
import CardPaint from './components/CardPaint.vue';
import GalleryAndInfoItem from './components/GalleryAndInfoItem.vue';
export default {
  // mounted() {
  //   this.customers = customers
    
  // },
  data() {
    return {
      currentItem: null,
      visible: false,
      customers: [
        { id: 1, name: "«Рождение Венеры»", author: " Сандро Боттичелли", oldSalary: '2 000 000 $', salary: '1 000 000 $', check: 1, itemMainImg: 'https://dl.dropboxusercontent.com/s/9u6q6122wrscql7/imgMain1.png?dl=0', firstImg: 'https://dl.dropboxusercontent.com/s/ey7rbl4gl34tcrb/1.jpg?dl=0', secondImg: 'https://dl.dropboxusercontent.com/s/j484fl17tktck6z/2.jpg?dl=0', thirdImg: 'https://dl.dropboxusercontent.com/s/ucm3lsccpn6gxor/3.jpg?dl=0', info: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Hic, assumenda!' },
        { id: 2, name: "«Тайная вечеря»", author: " Леонардо да Винчи", oldSalary: 'None', salary: '3 000 000 $', check: 1, itemMainImg: 'https://dl.dropboxusercontent.com/s/xq4cup6pdoyf8jy/imgMain2.png?dl=0', firstImg: 'https://dl.dropboxusercontent.com/s/fjq4fcu0ng9m897/1.jpg?dl=0', secondImg: 'https://dl.dropboxusercontent.com/s/whm0c3oxwmhuv3g/2.jpg?dl=0', thirdImg: 'https://dl.dropboxusercontent.com/s/o349v6hd9la2ufc/3.jpg?dl=0', info: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus eaque nobis consequatur, tenetur labore optio.' },
        { id: 3, name: '«Сотворение Адама»', author: ' Микеланджело', oldSalary: '6 000 000 $', salary: '5 000 000 $', check: 1, itemMainImg: 'https://dl.dropboxusercontent.com/s/43sml5p4wua8asc/imgMain3.png?dl=0', firstImg: 'https://dl.dropboxusercontent.com/s/uiv5q969d50fne5/1.jpg?dl=0', secondImg: 'https://dl.dropboxusercontent.com/s/c0s4a1owax4oioz/2.jpg?dl=0', thirdImg: 'https://dl.dropboxusercontent.com/s/se5p257gdkw1p83/3.jpg?dl=0', info: 'Lorem ipsum dolor sit amet consectetur adipisicing.' },
        { id: 4, name: '«Урок анатомии»', author: ' Рембрандт', oldSalary: 'None', salary: 'None', check: 1, itemMainImg: 'https://dl.dropboxusercontent.com/s/yq2d6vx0oya1npo/imgMain4.png?dl=0', firstImg: 'https://dl.dropboxusercontent.com/s/36hmh6oeltcj7ar/1.jpg?dl=0', secondImg: 'https://dl.dropboxusercontent.com/s/4l9vii3o1u0uko3/2.jpg?dl=0', thirdImg: 'https://dl.dropboxusercontent.com/s/takybavrtp4vx56/3.jpg?dl=0', info: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sint nihil assumenda veritatis.' }
      ]
    }
  },
  components: {
    Autocomlete,
    CardPaint,
    GalleryAndInfoItem
  },
  methods: {
    open(item) {
      this.currentItem = item
      this.visible = !this.visible
    },
    close() {
      this.visible = !this.visible
    },
    saveToLocalStorage(arr) {
      localStorage.setItem('list', JSON.stringify(arr));
    },
    custom(items){
      localStorage.clear()
      this.saveToLocalStorage(items)
    }
  },
  mounted(){
    const localItems = localStorage.getItem('list');
    if (localItems && localItems !== "undefined") {
      // customers.set(JSON.parse(localItems));
      console.log(JSON.parse(localStorage.getItem('list')))
      this.customers = JSON.parse(localStorage.getItem('list'))
    }
  }
}
</script>

<template>
  <div class="opacity-div" v-if="visible" @click="close"></div>
  <div class="modal-gallery-and-info" v-if="visible" @click="close">
    <div class="modal-gallery-and-info-wrapper" @click.stop>
      <GalleryAndInfoItem :item="currentItem" />
    </div>
  </div>
  <header>
    <nav class="nav-header">
      <a href="/">Каталог</a>
      <a href="/">Доставка</a>
      <a href="/">Оплата</a>
      <a href="/">Контакты</a>
      <a href="/">О компании</a>
    </nav>
    <Autocomlete :items="customers" filterby="name" class="search" />
  </header>
  <hr>
  <main>
    <div class="main-wrapper">
      <div class="name-holder">
        <h1>Картины эпохи Возрождения</h1>
      </div>
      <div class="list-items">
        <CardPaint :items="customers" @open="open" @custom = 'custom'/>
      </div>
    </div>
  </main>
  <footer>
    <div class="foo">
      <nav class="nav-footer">
        <a href="/">Каталог</a>
        <a href="/">Доставка</a>
        <a href="/">Оплата</a>
        <a href="/">Контакты</a>
        <a href="/">О компании</a>
      </nav>
      <div class="contacts">

        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 14 14" fill="none">
          <path
            d="M13.6861 11.0733L11.5241 8.9061C11.0934 8.47621 10.3803 8.48927 9.93461 8.9361L8.84534 10.0276C8.77652 9.98957 8.70529 9.94987 8.6304 9.90774C7.94254 9.52574 7.00109 9.00217 6.0104 8.00851C5.01678 7.01276 4.49391 6.06772 4.11161 5.37786C4.07127 5.30478 4.03261 5.23431 3.99445 5.16739L4.7255 4.43577L5.08492 4.07509C5.53125 3.62763 5.54356 2.91305 5.11392 2.48192L2.95184 0.314451C2.52219 -0.116083 1.80871 -0.103021 1.36238 0.344444L0.753032 0.95868L0.769684 0.975248C0.565361 1.23655 0.394623 1.53793 0.267564 1.86292C0.150441 2.17228 0.0775199 2.46748 0.0441767 2.76329C-0.241312 5.13542 0.840231 7.30337 3.7754 10.2452C7.8327 14.3114 11.1023 14.0043 11.2434 13.9893C11.5506 13.9525 11.845 13.8789 12.1442 13.7624C12.4657 13.6366 12.7662 13.4657 13.0267 13.2613L13.04 13.2732L13.6573 12.6673C14.1028 12.22 14.1156 11.5051 13.6861 11.0733Z"
            fill="#555555" />
        </svg>

        <a href="tel:+7(812)555-55-55" style="margin-left: 10px; width: 136px;">+7(812)555-55-55</a>
      </div>
      <div class="adres">

        <svg xmlns="http://www.w3.org/2000/svg" width="11" height="14" viewBox="0 0 11 14" fill="none">
          <path
            d="M5.07028 0C2.27451 0 0 2.27451 0 5.07025C0 8.53985 4.5374 13.6334 4.73058 13.8486C4.91204 14.0507 5.22884 14.0503 5.40997 13.8486C5.60315 13.6334 10.1406 8.53985 10.1406 5.07025C10.1405 2.27451 7.86601 0 5.07028 0ZM5.07028 7.62123C3.66366 7.62123 2.51932 6.47687 2.51932 5.07025C2.51932 3.66363 3.66368 2.51929 5.07028 2.51929C6.47687 2.51929 7.6212 3.66366 7.6212 5.07028C7.6212 6.47689 6.47687 7.62123 5.07028 7.62123Z"
            fill="#555555" />
        </svg>

        <a href="" style="margin-left: 10px; width: 261px;">г. Санкт-Петербург, ул. Ефимова, 3</a>
      </div>
    </div>
  </footer>
</template>

<style>
.opacity-div {
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: #343030;
  opacity: 0.75;
  z-index: 5;
}

.modal-gallery-and-info {
  position: fixed;
  width: 100%;
  height: 100%;
  z-index: 5;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-gallery-and-info-wrapper {
  width: 700px;
  height: 640px;
  background-color: #E1E1E1;
}

main {
  height: 76vh;
}

header {
  width: 1200px;
  margin: 0 auto;
  height: 97px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}

a {
  margin-left: 48px;
  text-decoration: none;
  color: #343030;
  font-family: 'Merriweather';
  font-style: normal;
  font-weight: 400;
  line-height: 21px;
  font-size: 14px;
}

.name-holder {
  width: 1200px;
  margin: 0 auto;
  height: 100px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.name-holder h1 {
  height: 36px;
  width: 390px;
  font-family: 'Merriweather';
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 150%;
}

hr {
  color: #E1E1E1;
}

.nav-header {
  width: 80%;
  display: flex;
  justify-content: center;
}

.search {
  height: 100%;
  width: 20%;
  display: flex;
  align-items: center;
}

.list-items {
  width: 1200px;
  margin: 0 auto;
}

footer {
  width: 100%;
  background: #ECEAEA;
}

.foo {
  width: 1200px;
  margin: 0 auto;
  height: 97px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}

.contacts {
  display: flex;
  align-items: center;
}

.adres {
  display: flex;
  align-items: center;
}
</style>
