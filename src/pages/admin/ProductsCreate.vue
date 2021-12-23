<template>
    <h3>Add Product : </h3>
    <form @submit.prevent="submit">
        <div class="form-groupe">
            <label>Title</label>
            <input v-model="title" class="form-control" name="title"/>
        </div>
         <div class="form-groupe">
            <label>Image</label>
            <input v-model="image" class="form-control" name="image"/>
        </div>
        <br>
        <button class="btn btn-success">Save</button>
    </form>
</template>

<script>
import {ref} from 'vue';
import {useRouter} from 'vue-router';
export default {
    name: "ProductsCreate",
    setup(){
        const title = ref('');
        const image = ref('');
        const router = useRouter();

        const submit = async() => {
            await fetch('http://localhost:8000/api/products/',{
                method: 'POST',
                headers: {'Content-type': 'application/json'},
                body: JSON.stringify({
                    title: title.value,
                    image: image.value,
                })
            });

            await router.push('/admin/products');
        }

        return{
            title,
            image,
            submit
        }
    }
}
</script>