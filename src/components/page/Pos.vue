<template>
     <div class="pos">
       <el-row>
              <el-col :span='7' class="pos_left" id="orderBox">
                    <el-tabs v-model="activeName" @tab-click="handleClick" >
                        <el-tab-pane label="点餐" name="first">
                             <el-table :data="tableData" border style="width: 100%">
                                    <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                                    <el-table-column prop="count" label="数量"  width="50"> </el-table-column>
                                    <el-table-column prop="price" label="金额" width="60" ></el-table-column>
                                    <el-table-column prop="name" label="操作" width="100" fixed="right">
                                        <template slot-scope="scope">
                                              <el-button type="text" size="small">添加</el-button>
                                              <el-button type="text" size="small">删除</el-button>
                                       </template>
                                    </el-table-column>
                              </el-table>
                            <!--点餐  挂单  外卖-->
                            <div style="margin: 20px 0">
                                  <el-button type="warning">挂单</el-button>
                                  <el-button type="danger">删除</el-button>
                                  <el-button type="success">结账</el-button>
                            </div>


                        </el-tab-pane>
                        <el-tab-pane label="挂单" name="second">2

                        </el-tab-pane>
                        <el-tab-pane label="外卖" name="third">3

                        </el-tab-pane>
                    </el-tabs>
              </el-col>
              <el-col :span='17'>
                    <div class="foods_list">
                          <div class="title">商品信息</div>
                      <div class="list">
                          <ul>
                            <li v-for = "val in goods" @click="addfoods(val)">
                              <span>{{val.goodsName}}</span>
                              <span class="o-price">￥{{val.price}}元</span>
                            </li>
                          </ul>
                      </div>
                    </div>
                    <div class="type_foods">
                  <el-tabs v-model="foodtypeName" @tab-click="handleClick" >
                      <el-tab-pane label="汉堡" name="first" >
                            <ul class='cookList'>
                                <li v-for = "item in typegoods[0]" @click="addfoods(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">￥{{item.price}}元</span>
                                </li>
                            </ul>
                      </el-tab-pane>
                      <el-tab-pane label="小食" name="second">
                            <ul class='cookList'>
                                <li v-for = "item in typegoods[1]" @click="addfoods(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">￥{{item.price}}元</span>
                                </li>
                            </ul>
                      </el-tab-pane>
                      <el-tab-pane label="饮料" name="third">
                            <ul class='cookList'>
                                <li v-for = "item in typegoods[2]" @click="addfoods(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">￥{{item.price}}元</span>
                                </li>
                            </ul>
                      </el-tab-pane>
                       <el-tab-pane label="套餐" name="four">
                            <ul class='cookList'>
                                <li v-for = "item in typegoods[3]" @click="addfoods(item)">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">￥{{item.price}}元</span>
                                </li>
                            </ul>
                      </el-tab-pane>
                  </el-tabs>
              </div>
              </el-col>


       </el-row>
    </div>
</template>

<script>
  window.onresize = function(){ //监听屏幕大小
        document.getElementById('orderBox').style.height =document.body.scrollHeight + 'px';
    }

import axios from 'axios'
export default {
  name: 'Pos',
  data () {
    return {
        activeName: 'first',
        foodtypeName:'first',
        tableData: [], //左侧选择的食品
        goods:[], //右侧上方商品信息
        typegoods:[],//右侧下方商品信息

    }
  },
  mounted(){
    document.getElementById('orderBox').style.height = document.body.scrollHeight + 'px';
 },
 created(){
      this.getgood();//右侧上方商品信息
      this.gettypegood(); //食品种类
 },
 methods: {
  //  选项卡切换
    handleClick(tab, event) {
        // console.log(tab, event);
      },

    //点击添加
    addfoods(val){
      var _this = this;
      var newdata={} //新的食品选择
      // console.log('加=>'+val.goodsId+val.goodsName+val.price);
      var ishave =  false;
        //判断有没有选择
      for(var i=0; i < _this.tableData.length; i++){
         console.log(_this.tableData[i].goodsId);
          if(_this.tableData[i].goodsId == val.goodsId){

            ishave = true; //说明选择了

          }
       }
       if(ishave){
         //说明选择了
        // var arr = this.tableData.filter(o =>o.goodsId == val.goodsId);
        var arr = this.tableData.filter(
            function(data){
              console.log('data=>'+data)
                  return data.goodsId == val.goodsId
          });
         arr[0].count++;

        //  o(o.goodsId == val.goodsId)
       }else{
            //说明没有选择
             newdata = {'goodsId':val.goodsId,'goodsName':val.goodsName,'price':val.price,'count':1}
            _this.tableData.push(newdata)
          }


    },


    // 获取到常用的食物列表
    getgood(){
        axios.get('http://jspang.com/DemoApi/oftenGoods.php')
        .then(response=>{
          console.log(response);
          this.goods=response.data;
        })
        .catch(error=>{
            console.log(error);
            alert('网络错误，不能访问');
        })
    },
    // 获取类型
    gettypegood(){
         axios.get('http://jspang.com/DemoApi/typeGoods.php')
        .then(response=>{
          console.log(response);
          this.typegoods=response.data;
        })
        .catch(error=>{
            console.log(error);
            alert('网络错误，不能访问');
        })
    },

 }

}
</script>
<style scoped>
  .pos_left{
      height: 100%;
      background-color: #F9FAFC;
      border-right: 1px solid #c0ccda;
  }
.foods_list{
  height: 38px;
  line-height: 38px;
  border-bottom: 2px solid #e4e7ed;
  background-color: #F9FAFC;
}
.title{
  font-weight: 700;
  margin-left: 10px;
  text-align: left
}
.list ul li{
  list-style: none;
  float:left;
  border:1px solid #E5E9F2;
  padding:10px;
  margin:5px;
  background-color:#fff;
  cursor: pointer;
}
.o-price{
      color:#58B7FF;
   }
.type_foods{
  clear: both;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor: pointer;

   }
   .cookList li span{

        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;

   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }

</style>
