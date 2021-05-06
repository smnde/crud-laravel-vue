<template>
    <div>
        <h2 class="text-center">List Products</h2>
        <!-- <div class="row">
            <div class="col-6 mx-auto"> -->
                <table class="table table-hover text-center">
                    <thead>
                        <tr>
                            <th>No</th>
                            <th>Name</th>
                            <th>Detail</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="product in products" :key="product.id">
                            <td>{{ product.id }}</td>
                            <td>{{ product.name }}</td>
                            <td>{{ product.detail }}</td>
                            <td>
                                <div class="btn-group" role="group">
                                    <router-link :to="{name: 'edit', params: {id: product.id}}" class="btn btn-success">Edit</router-link>
                                    <button class="btn btn-danger" @click="deleteProduct(product.id)">Delete</button>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            <!-- </div>
        </div> -->
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: [],
        }
    },
    created() {
        this.axios
            .get('http://laravue.test/api/products')
            .then(response => this.products = response.data);
    },
    methods: {
        deleteProduct(id) {
            this.axios
                .delete(`http://laravue.test/api/products/${id}`)
                .then(response => {
                    let i = this.products.map(data => data.id).indexOf(id);
                    this.products.splice(i, 1);
                })
        }
    },
}
</script>