<template>
    <v-col cols="4">
      <v-skeleton-loader
        v-if="loading"
        class="mx-auto"
        type="card, list-item-two-line"
      ></v-skeleton-loader>
      <div class="pr-partial" v-else>
        <div class="img" >
          <v-img v-if="product.whole == 0" min-height="200" @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" :src="product.ItemImage"></v-img>
          <v-img v-else min-height="200" @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" :src="product.ItemImageWhole"></v-img>
          <div class="actions">
             <v-btn
                class="mx-2"
                fab
                dark
                small
                @click.prevent="remove()"
                color="primary"
              >
                <v-icon dark>
                  mdi-trash-can-outline
                </v-icon>
              </v-btn>
              <v-btn
                class="mx-2"
                :class="{active : product.inCart}"
                fab
                dark
                small
                @click.prevent="switchToCart()"
                color="primary"
              >
                <v-icon dark>
                  mdi-cart-plus
                </v-icon>
              </v-btn>
          </div>
        </div>
        <div class="meta text-center">
          <div v-if="product.whole == 0">
            <h2 class="product-title pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-if="$i18n.locale == 'ar'">{{product.ItemName}}</h2>
            <h2 class="product-title  pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-else>{{product.ItemNameEn}}</h2>
          </div>
          <div v-else>
            <h2 class="product-title pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-if="$i18n.locale == 'ar'">{{product.ItemNameWhole}}</h2>
            <h2 class="product-title  pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-else>{{product.ItemNameEnWhole}}</h2>
          </div>
          <div class="price">
            <span class="text-primary text-sm">{{ $n(product.price, 'currency' , 'en') }}</span>
          </div>
        
        </div>
      </div>
    </v-col>
</template>

<script>
export default {
  props : ['loading' , 'product'],
  data () {
    return {
      qty : 1
    }
  },
  methods:{
    switchToCart(){
      this.$store.dispatch('wishlist/switch', {id : this.product.id , qty : 2})
    },
    remove(){
      this.$store.dispatch('wishlist/remove' , this.product.id)
    },
  }
}
</script>

<style scoped src="@/assets/scss/partials/product-partial.css"/>
