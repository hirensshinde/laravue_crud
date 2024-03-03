<template>
    <main>
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container-fluid">

                <router-link to="/" class="navbar-brand" href="#">
                    Laravel Vue Crud App
                </router-link>
                <div class="collapse navbar-collapse">
                    <div class="navbar-nav">
                        <router-link exact-active-class="active" to="/" class="nav-item nav-link">Home</router-link>
                        <router-link exact-active-class="active" to="/category"
                            class="nav-item nav-link">Category</router-link>
                    </div>
                </div>
            </div>
        </nav>
        <div class="container mt-5">
            <router-view></router-view>
        </div>
    </main>
</template>

<script>

export default {
    name: "categories",
    data() {
        return {
            categories: []
        }
    },
    mounted() {
        this.getCategories()
    },
    methods: {
        async getCategories() {
            await this.axios.get('/api/category').then(response => {
                this.categories = response.data
            }).catch(error => {
                console.log(error)
                this.categories = []
            })
        },
        deleteCategory(id) {
            if (confirm("Are you sure to delete this category ?")) {
                this.axios.delete(`/api/category/${id}`).then(response => {
                    this.getCategories()
                }).catch(error => {
                    console.log(error)
                })
            }
        }
    }
}
</script>
