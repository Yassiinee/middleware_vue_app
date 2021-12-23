<template>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<main>

  <section class="py-5 text-center container">
    <div class="row py-lg-5">
      <div class="col-lg-7 col-md-9 mx-auto">
        <h1 class="fw-light">Projet Middleware</h1>
        <h2 class="fw-light">Yassine Zakhama- Mohamed Ben Hlima</h2>
        <h3 class="fw-light">FIA2-GL-01</h3>
        <p class="lead text-muted">Vue JS , Laravel Microservices , RabbitMQ</p>
        <p>
            <router-link to="/admin/products/" class="btn btn-warning">Dashboard Admin Panel</router-link>
        </p>
      </div>
    </div>
  </section>

  <div class="album py-5 bg-light">
    <div class="container">

      <div class="row">
        <div class="col-md-4" v-for="product in products" :key="product.id">
          <div class="card mb-4 shadow-sm">
              <img :src="product.image" height="180"/>
            <div class="card-body">
              <p class="card-text">{{product.title}}</p>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group">
                  <button class="btn btn-primary" @click="like(product.id)"><i style="font-size:24px" class="fa">&#xf087;</i></button>
                </div>
                <small class="text-muted">{{product.likes}} likes</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</main>
</template>

<script lang="ts">
import {ref,onMounted} from 'vue';
import { Product } from '@/interfaces/product';
export default {
    name: "Main",
    setup() {
        const products = ref([] as Product[]);

        onMounted(async () => {
            const response = await fetch('http://localhost:8000/api/products');

            products.value = await response.json();
        });

        const like = async (id: number) => {
            await fetch(`http://localhost:8001/api/products/${id}/like`,{
                method: 'POST',
                headers: {'Content-type': 'application/json'},

            });

            products.value = products.value.map(
                (p: Product) => {
                    if(p.id == id) {
                        p.likes++;
                    }
                    return p;
                }
            );
        }

        return{
            products,
            like
        }
    }
}
</script>