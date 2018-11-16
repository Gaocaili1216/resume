<template>
    <div class="details">
        <div class="noPay-title">
                    <div class="toAdmin" @click="toAdmin()">&lt; 个人中心</div>
                </div>
            <div id="noPay_list" class="noPay_all">
                
                <div class="noPay_head">
                        <p style="color:black">订单号:{{oid}}</p>
                        <p style="color:black">下单时间：{{time | datetimeFilter}}</p> 
                </div>
                <div class="noPay_md">
                    <a href="#"><img src="http://127.0.0.1:3000/img/2.png" class="noPay_img"></a>
                    <p>订单已提交</p>
                </div>
                <div class="noPay_middle" >
                    <div class="noPay_details" v-for="item in list" :key="item.id">
                        <img :src="item.pic" class="detail_img">
                        <span class="noPay_1">x{{item.count}}</span>
                        <span class="noPay_guo">{{item.title}}</span>
                        <span class="noPay_price">￥<span class="price_m">{{item.price}}</span></span>
                    </div>   
                </div>
                <div class="detail-foot">
                    <div class="pay_foot">
                        <div class="all_price">合计：<span class="total_price">￥{{priceAll.toFixed(2)}}</span></div>
                    </div>
                    <div class="quick">
                        <router-link to="/pay" class="pay_price">立即支付</router-link>
                    </div>
                </div>

            </div>
            <order-nav></order-nav>
        </div>
        
    </div>
</template>
<script>
    import orderNav from "../Order/OrderNav.vue"
    export default {
        data(){
            return {
                list:[],
                oid:'',
                priceAll:0,
                time:'',
            }
        },
        methods:{
            nopay(){    
                var url="http://127.0.0.1:3000/formdetail?oid="+this.oid
                this.$http.get(url).then(result=>{
                    this.list=result.body
                    this.priceAll=0;
                    for(var i=0;i<this.list.length;i++){
                    this.priceAll+=this.list[i].count*this.list[i].price
                  }
                this.time=this.list[0].order_time
                })
            },
            toAdmin(){
                window.location.href=('http://127.0.0.1:3001/#/admin')
            }
        },
        created(){
            this.oid=this.$route.query.oid;
            this.nopay();
        },
        watch:{
            oid:function(){
                this.nopay()
            },
            list:function(){
                this.nopay()
            }
        },
        components:{
        "order-nav":orderNav,
        }
    }
</script>
<style>
  .toAdmin{
      margin:10px 15px;
      padding:5px 10px;
      background:rgba(0,0,0,.6);
      width:100px;
      font-size:16px;
      border-radius:16px;
      color:#fff;
  }
  .detail-foot{
      width:100%;
      height:40px;
      background:#fff;
  }
   .noPay{
    text-decoration:none;
    font-size:0.9rem;
    color:#1e1e1e;
 }       
 .quit{
     text-decoration:none;
     font-size:0.9rem;
     color:#1e1e1e;
 }
 .allList{
    text-decoration:none;
    font-size:0.9rem;
    color:#1e1e1e;
 }
 .top_all{
     margin-top:30px;
 }
 .active{
    color:#fc8a09;
    font-size:1.0rem;
 }
 
  .noPay_all{
    position:relative;
    background:white;
    padding-top:5px;
    width:95%;
    height:580px;
    margin:0 auto;
    margin-top:10px;
    border-radius:16px;
    box-shadow:1px 1px 5px 5px #ccc;
 }
 .noPay_all:active{
    width:100%;
    margin:0 auto;
 }    
 .details  .noPay_all .noPay_head {
    width:92%;
    margin:20px auto 20px;
    font-weight:bold;
    border-bottom:2px dashed black;
    padding-bottom:7px;color:#000;
 }
 .noPay_md{
    width:92%;
    margin:0 auto;
    height:30px;
 }
 .noPay_img{
    width:10%;
    float:left;
    margin-left:10px;
 }
 .noPay_md>p{
    float:right;
    font-size:0.9rem;
    color:#ff4042;
    padding-top:5px;
 }
 .noPay_middle{
     position:relative;
    width:92%;
    margin:0 20px;
    display:inline-block;
    margin-top:10px;
    padding-bottom:20px;
    border-top:1px solid #e5e5e5;
    border-bottom:1px solid #e5e5e5;
 }
 .noPay_details{
    width:92%;
    height:50px;
    margin-top:15px;
    position:relative;
 }
 .detail_img{
     width:50px;
    height:50px;
    float:left;
 }
 .noPay_1{
    font-size:0.7rem;
    float:left;
    margin-left:10px;
    position:absolute;
    bottom:0;
 }
 .noPay_guo{
    float:left;
    font-size:0.8rem;
    margin-left:10px;
 }
 .noPay_price{
    float:right;
    font-size:0.7rem;
 }
 .price_m{
    font-size:1.0rem;
    font-weight:700;
    margin-top:20px;
 }
 .pay_foot{
    width:92%;
    height:30px;
    float:left;
 }
 .all_price{
   font-size:0.9rem;
  
   margin-left:20px;
 }
 .total_price{
   font-size:1.0rem;
   font-weight:700;
 }
 .quick{
    width:92%;
    height:30px;
    margin-bottom:20px;
    position:absolute;
 }
 .pay_price{
   font-size:0.9rem;
   float:right;
   background:#ff4042;
   color:white;
   padding:7px 10px;
   text-decoration:none;
   border-radius:7px;
  }
 .all_quit{
    width:92%;
    height:170px;
    margin:0 auto;
    border:1px solid #e5e5e5;
    border-radius:3px;
    margin-top:10px;
    position:relative;
    box-shadow:3px -3px 4px #eeeeee;
    background:white;
    margin-top:110px;
    margin-bottom:60px;
    padding-top:10px
 }
</style>