<template>
     <div class="pos">
       <el-row>
              <el-col :span='7' class="pos_left" id="orderBox">
                    <el-tabs v-model="activeName" @tab-click="handleClick" >
                        <el-tab-pane label="点餐" name="first">
                             <el-table :data="tableData" border style="width: 100%">
                                    <el-table-column prop="name" label="商品名称"></el-table-column>
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
                            <li v-for = "val in goods">
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
                                <li v-for = "item in typegoods">
                                    <span class="foodImg"><img :src="item.goodsImg" width="100%"></span>
                                    <span class="foodName">{{item.goodsName}}</span>
                                    <span class="foodPrice">￥{{item.price}}元</span>
                                </li>
                            </ul>
                      </el-tab-pane>
                      <el-tab-pane label="小食" name="second">2

                      </el-tab-pane>
                      <el-tab-pane label="饮料" name="third">3

                      </el-tab-pane>
                       <el-tab-pane label="套餐" name="four">4

                      </el-tab-pane>
                  </el-tabs>
              </div>
              </el-col>


       </el-row>
    </div>
</template>

<script>
  window.onresize = function(){ //监听屏幕大小
        document.getElementById('orderBox').style.height =document.body.clientHeight + 'px';
    }
export default {
  name: 'Pos',
  data () {
    return {
         activeName: 'first',
         foodtypeName:'first',
       tableData: [
        {
          name: '可口可乐',
          count: '1',
          price: '10'
        },
        {
          name: '可口可乐',
          count: '1',
          price: '10'
        },
        {
          name: '可口可乐',
          count: '1',
          price: '10'
        },
        {
          name: '可口可乐',
          count: '1',
          price: '10'
        }
        ],
        goods:[
          {
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
              goodsName:'香脆鸡柳',
              price:17
          }
      ],
       typegoods:[
          {
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }

      ],

    }
  },
  mounted(){
    document.getElementById('orderBox').style.height = document.body.clientHeight + 'px';
 },
 methods: {
    handleClick(tab, event) {
        // console.log(tab, event);
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
