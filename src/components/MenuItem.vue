<template>
    <div class="menu-item">
        <img :src="image.source" :alt="image.alt" class="menu-item__image">
        <div>
            <h3>{{ name }}</h3>
            <p>Prix : {{ generatePrice }}</p>
            <p v-if="inStock">En stock</p>
            <p v-else>En rupture de stock</p>
			<div>
				<label for="add-item-quantity">Quantité : {{ quantity }}</label>
				<input v-model.number="quantity" id="add-item-quantity" type="number" />
				<button @click="updateShoppingCart(quantity)">
					Ajouter au panier
				</button>
			</div>
        </div>
    </div>
</template>

 
<script>
export default {
	name: "MenuItem",
    // props: ["addToShoppingCart", "image", "inStock", "name", "quantity", "price"],
    props:{
        image: {
            type: Object,
            required: true
        },
        inStock: {
            type: Boolean,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        quantity: {
            type: Number,
            default:1
        },
        price:{
            type : Number,
            required: true
        }
    },
    data(){
        return {
            onSale:false
        }
    },
    computed: {
        generatePrice(){
            if(this.onSale){
                return (this.price *0.9).toFixed(2)
            }else{
                return this.price
            }
        } 
    },
    beforeMount(){
            const today = new Date().getDate()

            if(today % 2 === 0 ){
                this.onSale = true
            }
    },
    methods:{
        updateShoppingCart(quantity){
            this.$emit('add-item-to-cart', quantity)
        }
    }
}
</script>

<style scoped>


.menu {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.menu-item {
  display: flex;
  width: 500px;
  justify-content: space-between;
  margin-bottom: 30px;
}

.menu-item__image {
  max-width: 300px;
}
h3{
    color : red;
}

</style>