<template>
    <div id="all-products">
        <h1 style="font-weight:bold; text-align: center;">Liste des produits</h1>

        <p><router-link :to="{ name: 'create_product' }" class="btn btn-primary">Créer un produit</router-link></p>

        <div class="form-group">
            <input type="text" name="search" v-model="productSearch" placeholder="chercher un produit" class="form-control" v-on:keyup="searchProducts">
        </div>

        <table class="table table-hover" style=" overflow : hidden; border-radius : 5px; box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);">
            <thead>
            <tr style="color : white; font-weight : bold; background: #060411 ">
        <!--    <td>ID</td> -->
                <td>Produit</td>
                <td>Date</td>
                <td>marque</td>
                <td>Fournisseur</td>
                <td>Prix</td>
                <td>Actions</td>
            </tr>
            </thead>

            <tbody>
                <tr v-for="product in products" v-bind:key="product.id">
             <!--   <td>{{ product.id }}</td> -->
                    <td>{{ product.name }}</td>
                    <td>{{ product.date }}</td>
                    <td>{{ product.mark }}</td>
                    <td>{{ product.supplier }}</td>
                    <td>{{ product.price }}</td>
                    <td>
                        <router-link :to="{name: 'edit_product', params: { id: product.id }}" class="btn btn-outline-primary" style="">Modifier</router-link>
                        <router-link :to="{name: 'delete_product', params: { id: product.id }}" class="btn btn-outline-danger">Supprimer</router-link>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

    export default{
        data(){
            return{
                products: [],
                originalProducts: [],
                productSearch: ''
            }
        },

        created: function()
        {
            this.fetchProductData();
        },

        methods: {
            fetchProductData: function()
            {//https://kaptan-app.herokuapp.com/ --- http://localhost:8080
                this.$http.get('https://kaptan-app.herokuapp.com/api/products').then((response) => {
                    this.products = response.body;
                    this.originalProducts = this.products;
                }, (response) => {

                });
            },

            searchProducts: function()
            {
                if(this.productSearch == '')
                {
                    this.products = this.originalProducts;
                    return;
                }

                var searchedProducts = [];
                for(var i = 0; i < this.originalProducts.length; i++)
                {
                    var productName = this.originalProducts[i]['name'].toLowerCase();
                    if(productName.indexOf(this.productSearch.toLowerCase()) >= 0)
                    {
                        searchedProducts.push(this.originalProducts[i]);
                    }
                }

                this.products = searchedProducts;
            }
        }
    }
</script>
