<template>
    <div>
        <div class="gallery-item">
            <div class="slider">
                <div class="images">
                    <input type="radio" name="slide" id="img1" checked>
                    <input type="radio" name="slide" id="img2">
                    <input type="radio" name="slide" id="img3">
                    <input type="radio" name="slide" id="img4">

                    <img :src="item.itemMainImg" class="m1" alt="img1">
                    <img :src="item.firstImg" class="m2" alt="img2">
                    <img :src="item.secondImg" class="m3" alt="img3">
                    <img :src="item.thirdImg" class="m4" alt="img4">
                </div>
                <div class="dots">
                    <label for="img1"></label>
                    <label for="img2"></label>
                    <label for="img3"></label>
                    <label for="img4"></label>
                </div>
            </div>
        </div>
        <div class="info-name-item">
            <h1>{{item.name + ' ' + item.author}}</h1>
        </div>
        <div class="info-item">
            <div class="description-item">
                <p><h3>{{item.info}}</h3></p>
            </div>
            <div class="salary-item">
                <h4>{{(item.oldSalary !== "None") ? item.oldSalary : ""}}</h4>
                <h3>{{(item.salary !== "None") ? item.salary : ""}}</h3>
                <div class="saled-item" v-if="(item.salary === 'None')">
                    <h2>Продана</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['item'],
    data() {
        return {
            
        }
    }
}
</script>

<style>

.info-name-item{
    margin: 15px 0px;
    width: 100%;
    display: flex;
    justify-content: center;
}

.info-item{
    display: flex;
}

.description-item{
    width: 70%;
    display: flex;
    align-items: center;
    justify-content: space-around;
}

.description-item h3{
    margin-left: 30px;
}

h4{
    text-decoration: line-through;
    color: #A0A0A0;
}

.salary-item{
    width: 30%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
    position: relative;
}

.saled-item{
    position: absolute;
    top: 0;
    opacity: 0.6;
}

.gallery-item{
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    /* background: rgb(170, 165, 175); */
    background: #403432;
}
.slider {
    position: relative;
    width: 80%;
    overflow: hidden;
}
.images {
    height: 450px;
    display: flex;
    align-items: center;
    width: 100%;
}
.images img {
    height: 400px;
    width: 100%;
    transition: all 0.15s ease;
}
.images input {
    display: none;
}
.dots {
    display: flex;
    justify-content: center;
    margin: 5px;
}
.dots label {
    height: 20px;
    width: 20px;
    border-radius: 50%;
    border: solid #fff 3px;
    cursor: pointer;
    transition: all 0.15s ease;
    margin: 5px;
}
.dots label:hover {background: #fff;}
#img1:checked ~ .m1 {
    margin-left: 0;
}
#img2:checked ~ .m2 {
    margin-left: -100%;
}
#img3:checked ~ .m3 {
    margin-left: -200%;
}
#img4:checked ~ .m4 {
    margin-left: -300%;
}
</style>