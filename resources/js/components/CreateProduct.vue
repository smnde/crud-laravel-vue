<template>
    <div>
        <h3 class="text-center">Create Product</h3>

        <div class="row">
            <div class="col-6">
                <form @submit.prevent="addProduct">
                    <div class="form-group">
                        <label for="name">Name</label>
                        <input type="text" v-model="product.name" class="form-control">
                    </div>
                    <div class="form-group">
                        <label for="detail">Detail</label>
                        <input type="text" v-model="product.detail" class="form-control">
                    </div>
                    <button type="submit" class="btn btn-primary">Create</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            product: {}
        }
    },
    methods: {
        addProduct() {
            this.axios
                .post('http://laravue.test/api/products/', this.product)
                .then(response => (
                    this.$router.push({name: 'home'})
                ))
                .catch(err => console.log(err))
                .finally(() => this.loading = false);
        }
    }
}
</script>