<template>
    <div>
      <v-skeleton-loader
        v-if="loading"
        class="mx-auto"
        type="card, list-item-two-line"
      ></v-skeleton-loader>
      <div class=" p-4 d-flex pr-partial" v-else>
        <div class="img mr-4"  >
          <v-img  v-if="product.whole == 0" width="100" @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" :src="product.ItemImage"></v-img>
          <v-img  v-else width="100" @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" :src="product.ItemImageWhole"></v-img>
          
        </div>
        <div class="meta">
          <div v-if="product.whole == 0">
          <h2 class="product-title pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-if="$i18n.locale == 'ar'">{{product.ItemName}}</h2>
          <h2 class="product-title  pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-else>{{product.ItemNameEn}}</h2>
          </div>
          <div v-else>
          <h2 class="product-title pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-if="$i18n.locale == 'ar'">{{product.ItemNameWhole}}</h2>
          <h2 class="product-title  pointer mb-2"  @click.prevent="$router.push({name : `shop-id___${$i18n.locale}` , params : {id : product.id}})" v-else>{{product.ItemNameEnWhole}}</h2>
          </div>
          <div class="price">
            <!-- <del class="text-sm">{{ $n(120, 'currency' , 'en') }}</del> -->
            <span class="text-primary">{{ $n(product.price, 'currency' , 'en') }}</span>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
// import { qtyss , wieghts } from '@/utilities/updateQty.js'
import updateCart from '@/mixins/updateCart.js'
export default {
  props : ['loading' , 'product'],
  mixins : [updateCart]
}
</script>

<style scoped src="@/assets/scss/partials/product-partial.css"/>
