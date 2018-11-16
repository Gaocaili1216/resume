<template>
    <div class="all-Container">
        <div class="noPay-title">
                    <div class="toAdmin" @click="toAdmin()">&lt; 个人中心</div>
                </div>
        <div class="details"> 
            <div id="all_list" class="top_all"> 
                <div class="all_1" v-for="item of list">
                        <div class="guo_1" @click="toDetail(item.orderform_id)">
                            <img src="http://127.0.0.1:3000/img/pot_071.jpg" alt="">
                            <span class="guo_1_l">订单编号：<span v-text="item.orderform_id"></span></span>
                            
                        </div>
                        <p class="guo_1_r">{{item.order_time | datetimeFilter}}</p>
                        <div class="guo_1_foo">
                            <div class="guo_1_f">实付：
                                <span class="guo_1_foot">￥<span v-text="item.total"></span> </span>
                            </div>
                        </div>
                        <div class="guo_1_lst">
                            <a href="#" class="guo_1_last">再来一单</a>
                        </div>
                </div>
            </div>
        </div>
        <order-nav></order-nav>
    </div>
</template>
<script>
  import orderNav from "../Order/OrderNav.vue"
  export default {
      data(){
          return {
              list:[],
              uid:''
          }
      },
      methods:{
          getList(){
              var url="http://127.0.0.1:3000/formlist?uid="+this.uid;
              this.$http.get(url).then(result=>{
                  this.list=result.body;
                    var time=this.list[0].order_time;
                    time=time.toString();
                    var year=time.slice(0,4)
              })
            },
            toAdmin(){
                    window.location.href=('http://127.0.0.1:3001/#/admin')
            },
            toDetail(oid){
                var url='http://127.0.0.1:3001/#/formdetail?oid='+oid
                window.location.href=(url)
            }
      },
      created(){
         this.uid=sessionStorage.getItem("uid")
         this.getList()
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
  .all_1{
    width:92%;
    height:170px;
    margin:0 auto;
    border:1px solid #e5e5e5;
    border-radius:12px;
    position:relative;
    box-shadow:2px 2px 3px 1px #ccc;
    background:white;
    margin-bottom:10px;
 }
  .guo_1{
   width:100%; 
   position:absolute;
    left:20px;
    top:30px;
 }
 .guo_1>img{
    width:23%;
    float:left;
 }    
 .guo_1_l{
    width:30%;
    padding:0 0 0 20px;
    font-size:0.9rem;
    color:#1e1e1e;
 }    

 .guo_1_foo{
   width:100%;
   margin:5px 0; 
   position:absolute;
   top:80px;
   right:20px;
 }
 .guo_1_f{
    width:40%;
    font-size:0.9rem;
    color:#1e1e1e;
    float:right;
    text-align:center;
 }
 .guo_1_foot{
    font-weight:bold;
    font-size:1.0rem;
    color:red;
 }
 .guo_1_lst{
    width:100%;
    position:absolute;
    bottom:20px;
    right:20px;
 }
 .guo_1_last{
    width:25%; 
    border:1px solid #e5e5e5;
    text-decoration:none;
    font-size:0.9rem;
    color:#1e1e1e;
    padding:5px 0;
    float:right;
    text-align:center;
    color:white;
    background:#ff4041;
    border-radius:6px;
 }
  .guo_1_r{
      position:absolute;
      top:50px;
      left:120px;
      text-align:right;
      padding-right:20px;
  }
   .app-container{
     overflow-x:hidden;
     height:100%;
   }
   .headList{
     width:100%;
     height:50px;
     position:fixed;
     top:0;
     left:0;
     z-index:999;
     background:#ff4042;
   }
 h5.bList{
    text-align:center;
    color:white;
    font-size:1.2rem;
    line-height:50px;
 }  

 div.main{
     width:100%;
     position:fixed;
     top:0;
     left:0;
     z-index:999;
     margin-top:40px;
 }
 .orderList{
    display:flex;
    flex-wrap:nowrap;
    text-align:center;
    background:#eee;
    margin:0;
    line-height:50px;
 }
 .orderList>li{
     list-style:none;
 }
 .orderList>li:last-child{
     width:33.3%;
 }
 .orderList>li:nth-child(2){
     width:33.3%;
 }
 .orderList>li:first-child{
     width:33.3%;
 } 
 
</style>