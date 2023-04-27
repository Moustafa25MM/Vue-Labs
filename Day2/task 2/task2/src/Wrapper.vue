<template>
    <div class="container border border-danger border-1" >
        <div class="row">
            <div class="col-12">
                <Header/>    
            </div>
        </div>
        <div class="row">
            <div class="col-4">
                    <Links/>    
            </div>
            <div class="col-8">
                    <Body/>    
            </div>
            
        </div>
        <div class="row">
            <div class="col-12">
                <Footer/>    
            </div>
        </div>
    </div>
</template>

<script>
import Header from './components/Header.vue';
import Footer from './components/Footer.vue'
import Links from './components/Links.vue'
import Body from './components/Body.vue'


export default {
  
  components: {
    Header,
    Footer,
    Links,
    Body,

  }
}
</script>


