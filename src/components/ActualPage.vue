<template>
    <div>
        <div class="nav-bar"></div>
        <div class="product">
            <div class="product-image" >
                <img v-bind:src="image"> 
            </div>
            <div class="Product-Name">

                <h1>{{kind}}</h1>
                <p v-if="isStock" class="stock">In Stock</p>
                <p v-else class="stock">Out of Stock</p>
                <p>Shipping: {{ shipping }}</p>



                <ul v-for="detail in details" :key="detail.detId">
                    <li >{{detail.detailName}}</li>
                </ul>

                <div v-for="(variant, index) in variants "
                 :key="variant.varId"
                 class="color-box" 
                 :style="{ backgroundColor: variant.varColor }"
                 @mouseover="updateProduct(index)"
                 >
                </div>

                <button 
                @click="addToCart()" 
                :disabled="!isStock"
                :class="{disabledButton: !isStock}"
                >
                Add to cart</button>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'actual-page',
    props: {
        premium: {
            type: Boolean,
            required: true
        }
    },
    data() {
        return {
            kind: 'Shoe',
            productIndex : 0,  
            details: [ 
                {
                    detId: 1,
                    detailName: 'High class'
                },
                
                {
                    detId: 2,
                    detailName: 'Water proof'
                },
                
                {
                    detId: 3,
                    detailName: 'New'
                }
            ],   
            variants: [
                {
                    varId: 21,
                    varColor: 'Blue',
                    varImage: require('@/assets/logo.png'),
                    varQuantity: 10
                },
                {
                    varId: 23,
                    varColor: 'Orange',
                    varImage: require('@/assets/o.png'),
                    varQuantity: 0
                },
            ],
            reviews: [],
        }
    },
    methods:{
        addToCart(){
            this.$emit('add-to-cart', this.variants[this.productIndex].varId)
        },
        updateProduct(index){
            this.productIndex = index
        },
        addReview(pR){
            this.reviews.push(pR)
        }
    },
    computed: {
        image(){
            return this.variants[this.productIndex].varImage
        },
        isStock(){
            return this.variants[this.productIndex].varQuantity
        },
        shipping(){
            if (this.premium) {
                return 'free' 
            } else {
                return 2.99
            }
        }
    }
}
</script>
 
<style >

*{
    box-sizing: border-box; padding: 0; margin: 0; 
}
 
body {
    font-family: Arial, Helvetica, sans-serif;
}
.nav-bar {
    background-color: #fba72c; width: 100%; height: 85px;
    margin: 0; padding: 0;
}

.product-image img{
    width:30%; height: 23%;
    padding: 30px;
}

.Product-Name{
 font-size: 2rem;
 position: absolute; top: 30%; left: 34%;
}

.stock{
    font-size: 1.5rem; border-radius: 5px;
    background-color: rgb(238, 207, 162);
    display: inline; padding: 4px;
}

.color-box{
    width: 40px; height: 40px; margin-top: 8px;
}

.boxs{
        width: 100px; height: 100px; margin-top: 8px;
}

button{
    font-size: 1.3rem;
    background-color: #24a0ed; color: #fff;
    border-radius: 8px;
    padding: 9px; margin: 7px;
    border: none;
    float: right;
}

.disabledButton{
    background-color: #d3d3d3;
    color: black;
}

</style>