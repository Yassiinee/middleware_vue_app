<template>
    <Nav/>

    <div class="container-fluid">
        <div class="row">
            <Menu/>

            <main role="main" class="col-md-9 ml-sm-auto col-lg-10 px-md-4">
                
                <router-view/>

            </main>
        </div>
    </div>
</template>

<script>
import Nav from "@/components/Nav";
import Menu from "@/components/Menu";
export default {
    name: "Admin",
    components:{
        Menu,
        Nav
    }
}
</script>