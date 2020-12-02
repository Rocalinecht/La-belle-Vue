<template>
 <div id="app" class="app">
		<h1>{{ restaurantName }}</h1>
		<p class="description">
			Bienvenue dans notre café {{ restaurantName }}! Nous sommes réputés pour
			notre pain et nos merveilleuses pâtisseries. Faites vous plaisir dès le
			matin ou avec un goûter réconfortant. Mais attention, vous verrez qu'il
			est difficile de s'arrêter.
		</p>

		<section class="menu">
			<h2>Menu</h2>
			<MenuItem
				v-for="item in simpleMenu"
				@add-item-to-cart="addToShoppingCart"
				:name="item.name"
				:image="item.image"
				:quantity="item.quantity"
				:inStock="item.inStock"
				:key="item.name"
        :price="item.price"
			/>
		</section>

		<aside class="shopping-cart">
			<h2>Panier d'achat : {{ shoppingCart }} articles</h2>
		</aside>

		<footer class="footer">
			<p>{{ copyright }}</p>
		</footer>
	</div>
</template>

<script>
// @ is an alias to /src
import MenuItem from "../components/MenuItem"
export default {
	name: "Home",
	components: {
		MenuItem
	},
	data() {
		return {
			restaurantName: "La belle Vue",
			shoppingCart: 0,
			simpleMenu: [
				{
					name: "Croissant",
					image: {
						source: "croissant.jpg",
						alt: "Un croissant"
					},
          inStock: true,
          price:3.05,
					quantity: 1
				},
				{
					name: "Baguette de pain",
					image: {
						source: "french-baguette.jpeg",
						alt: "Quatre baguettes de pain"
					},
          inStock: true,
          price:1.50,
					quantity: 1
				},
				{
					name: "Éclair",
					image: {
						source: "eclair.jpg",
						alt: "Éclair au chocolat"
					},
          inStock: false,
          price:2.10,
					quantity: 1
				}
			]
		}
	},
	computed: {
		copyright() {
			const currentYear = new Date().getFullYear()
			return `Copyright ${this.restaurantName} ${currentYear}`
		}
	},
	methods: {
		addToShoppingCart(amount) {
			this.shoppingCart += amount
		}
	}
}

</script>
