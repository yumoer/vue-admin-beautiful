<template>
  <div>
    <div class="crumbs">
      <el-breadcrumb separator=">">
        <el-breadcrumb-item to="/skuList"><i class="el-icon-lx-text"></i> SKU列表</el-breadcrumb-item>
        <el-breadcrumb-item>{{id !== undefined ? '编辑' : '新增'}}</el-breadcrumb-item>
      </el-breadcrumb>

    </div>
    <div class="container">
      <el-form ref="addFrom" :rules="rules" :model="addFrom" label-width="100px">
        <el-form-item label="商品名称" prop="name">
          <el-input v-model="addFrom.name" style="width:350px" placeholder="请输入商品名称"></el-input>
        </el-form-item>
        <el-form-item label="副标题">
          <el-input v-model="addFrom.caption" style="width:350px" placeholder="请输入副标题"></el-input>
        </el-form-item>
        <!--<el-form-item label="商品" prop="goods_id">
          <el-select v-model="addFrom.goods_id" filterable  placeholder="请搜索商品">
            <el-option
              v-for="item in tableData"
              :key="item.id"
              :label="item.name"
              :value="item.id">
            </el-option>
          </el-select>
        </el-form-item>-->
        <el-form-item label="从属类别" v-if="this.id !== undefined">
          <el-input disabled v-model="addFrom.category" style="width:350px" placeholder="请输入分组类别"></el-input>
        </el-form-item>

        <el-form-item label="商城售价" prop="price">
          <el-input v-model="addFrom.price" style="width:350px" placeholder="请输入商城售价"></el-input>
        </el-form-item>
        <el-form-item label="天津供价" prop="cost_price">
          <el-input v-model="addFrom.cost_price" style="width:350px" placeholder="请输入天津供价"></el-input>
        </el-form-item>
        <el-form-item label="市场价" prop="market_price">
          <el-input v-model="addFrom.market_price" style="width:350px" placeholder="请输入市场价"></el-input>
        </el-form-item>
        <el-form-item label="库存" prop="stock">
          <el-input v-model="addFrom.stock" style="width:350px" placeholder="请输入库存"></el-input>
        </el-form-item>
        <el-form-item label="销量" prop="sales">
          <el-input v-model="addFrom.sales" style="width:350px" placeholder="请输入销量"></el-input>
        </el-form-item>
        <el-form-item label="评价数" prop="comments">
          <el-input v-model="addFrom.comments" style="width:350px" placeholder="请输入评价数"></el-input>
        </el-form-item>

        <el-form-item label="是否上架销售" prop="is_launched">
          <el-radio-group v-model="addFrom.is_launched">
            <el-radio :label="true" :value="true">是</el-radio>
            <el-radio :label="false" :value="false">否</el-radio>
          </el-radio-group>
        </el-form-item>

        <el-form-item label="默认图片" v-if="id !== undefined">
          <el-input disabled v-model="addFrom.default_image_url" style="width:350px" placeholder="请输入默认图片地址"></el-input>
        </el-form-item>
        <el-form-item label="延保服务">
          <el-input v-model="addFrom.yanbao" style="width:350px" placeholder="请输入延保服务"></el-input>
        </el-form-item>
        <el-form-item label="型号" prop="goods_model">
          <el-input v-model="addFrom.goods_model" style="width:350px" placeholder="请输入型号"></el-input>
        </el-form-item>
        <el-form-item label="重量">
          <el-input v-model="addFrom.weight" style="width:350px" placeholder="请输入重量"></el-input>
        </el-form-item>
        <el-form-item label="产地">
          <el-input v-model="addFrom.product_area" style="width:350px" placeholder="请输入产地"></el-input>
        </el-form-item>
        <el-form-item label="条形码">
          <el-input v-model="addFrom.upc" style="width:350px" placeholder="请输入条形码"></el-input>
        </el-form-item>
        <el-form-item label="销售单位" prop="unit">
          <el-input v-model="addFrom.unit" style="width:350px" placeholder="请输入销售单位"></el-input>
        </el-form-item>

        <el-form-item label="是否促销产品" prop="sale_actives">
          <el-radio-group v-model="addFrom.sale_actives">
            <el-radio :label="true">是</el-radio>
            <el-radio :label="false">否</el-radio>
          </el-radio-group>
        </el-form-item>

        <el-form-item label="商品类型" prop="genre">
          <el-select v-model="addFrom.genre" placeholder="请选择商品类型">
            <el-option label="配件" :value="0"></el-option>
            <el-option label="服务" :value="1"></el-option>
            <el-option label="商品" :value="2"></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="规格详细参数" :prop="addFrom.spec_params" placeholder="请输入规格详细参数">
          <el-input
            type="textarea"
            :autosize="{ minRows: 4, maxRows: 4}"
            placeholder="请输入包装清单"
            v-model="addFrom.desc_ware">
          </el-input>
        </el-form-item>
        <el-form-item label="限制购买数量">
          <el-input v-model="addFrom.purchase_restriction" style="width:350px" placeholder="请输入限制购买数量"></el-input>
        </el-form-item>
        <el-form-item label="是否节能" prop="energy">
          <el-radio-group v-model="addFrom.energy">
            <el-radio :label="1" :value="1">是</el-radio>
            <el-radio :label="0" :value="0">否</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="是否环保" prop="protection">
          <el-radio-group v-model="addFrom.protection">
            <el-radio :label="1" :value="1">是</el-radio>
            <el-radio :label="0" :value="0">否</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="是否进口" prop="imported">
          <el-radio-group v-model="addFrom.imported">
            <el-radio :label="1" :value="1">是</el-radio>
            <el-radio :label="0" :value="0">否</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="对接单位" prop="supply_unit">
          <el-select v-model="addFrom.supply_unit" placeholder="请选择商品类型">
            <el-option label="电商" :value="0"></el-option>
            <el-option label="天津" :value="1"></el-option>
            <el-option label="央采" :value="2"></el-option>
          </el-select>
        </el-form-item>
        <!--<el-form-item label="所属单位" prop="source">
          <el-input v-model="addFrom.source" style="width:350px" placeholder="请输入所属单位"></el-input>
        </el-form-item>-->
      </el-form>
      <el-form style="position: fixed;right:100px;bottom: 20px;z-index: 1">
        <el-form-item >
          <el-button class="editor-btn" type="primary" @click="submitForm()">{{id !== undefined?'修改':'保存'}}</el-button>
          <el-button class="editor-btn" @click="goBack()">返回上一页</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
  import {SkuDetails,SpuList,SkuaddDetails,SkueditDetails} from '../../../api/index'
  export default {
    name: 'editor',
    data: function(){
      return {
        query: {
          page:1,
          page_size:99999,
          ordering:'-create_time',

        },
        tableData:[],
        addFrom:{},
        id:null,
        rules: {
          name: [
            { required: true, message: '请输入商品名称', trigger: 'blur' },
          ],
          goods_id: [
            { required: true, message: '请选择SPU商品', trigger: 'blur' }
          ],
          price: [
            { required: true, message: '请选择商城售价', trigger: 'blur' }
          ],
          market_price: [
            { required: true, message: '请选择市场价', trigger: 'blur' }
          ],
          cost_price: [
            { required: true, message: '请选择天津供货价', trigger: 'blur' }
          ],
          stock: [
            { required: true, message: '请输入库存', trigger: 'blur' }
          ],
          sales: [
            { required: true, message: '请输入销量', trigger: 'blur' }
          ],
          comments: [
            { required: true, message: '请输入评论数', trigger: 'blur' }
          ],
          goods_model: [
            { required: true, message: '请选择型号', trigger: 'blur' }
          ],
          unit: [
            { required: true, message: '请选择销量单位', trigger: 'blur' }
          ],
        }
      }
    },
    created(){
      this.id = this.$route.query.id
      this.addFrom.goods_id = this.$route.query.skuId
      console.log(this.id,+this.addFrom.goods_id)
      this.getShop()
      if(this.id !== undefined){
        this.getData()
      }else{
        this.addFrom = {
          genre:0,
          protection:0,
          energy:0,
          imported:0,
          supply_unit:0,
          sale_actives:false,
          is_launched:true,
        }
      }

    },
    activated(){
      this.id = this.$route.query.id
      this.addFrom.goods_id = this.$route.query.skuId
      console.log(this.id,+this.addFrom.goods_id)
      this.getShop()
      if(this.id !== undefined){
        this.getData()
      }else{
        this.addFrom = {
          genre:0,
          protection:0,
          energy:0,
          imported:0,
          supply_unit:0,
          sale_actives:false,
          is_launched:true,
        }
      }
    },
    methods: {
      getData(){
        SkuDetails(this.id).then(res => {
          console.log(res);
          this.addFrom = res.data;
        }).catch(error=>{
          if (error.response !== undefined) {
            switch (error.response.status) {
              case 500:
                this.$message.error('服务器错误')
                break
              case 401:
                this.$message.error('登录过期，请重新登录')
                localStorage.removeItem('ms_userInfo')
                break
              case 403:
                this.$message.error('您没有执行该操作的权限')
                break
              default:
                this.$message.error('其他错误')
                break
            }
          }
        });
      },

      getShop(){
        SpuList(this.query).then(res => {
          console.log(res);
          this.tableData = res.data.results;
        }).catch(error=>{
          if (error.response !== undefined) {
            switch (error.response.status) {
              case 500:
                this.$message.error('服务器错误')
                break
              case 401:
                this.$message.error('登录过期，请重新登录')
                localStorage.removeItem('ms_userInfo')
                break
              case 403:
                this.$message.error('您没有执行该操作的权限')
                break
              default:
                this.$message.error('其他错误')
                break
            }
          }
        });
      },

      getAdd(){
        SkuaddDetails(this.addFrom).then(res=>{
          console.log(res)
          if(res.status === 201){
            this.$message.success('保存成功')
            this.$router.go(-1)
          }
        }).catch(error=>{
          if (error.response !== undefined) {
            switch (error.response.status) {
              case 500:
                this.$message.error('服务器错误')
                break
              case 401:
                this.$message.error('登录过期，请重新登录')
                localStorage.removeItem('ms_userInfo')
                break
              case 403:
                this.$message.error('您没有执行该操作的权限')
                break
              default:
                this.$message.error('其他错误')
                break
            }
          }
        })
      },

      getEdit(){
        SkueditDetails(this.addFrom).then(res=>{
          console.log(res,res.status)
          if(res.status === 200){
            this.$message.success('修改成功')
            this.$router.go(-1)
          }
        }).catch(error=>{
          if (error.response !== undefined) {
            switch (error.response.status) {
              case 500:
                this.$message.error('服务器错误')
                break
              case 401:
                this.$message.error('登录过期，请重新登录')
                localStorage.removeItem('ms_userInfo')
                break
              case 403:
                this.$message.error('您没有执行该操作的权限')
                break
              default:
                this.$message.error('其他错误')
                break
            }
          }
        })
      },

      submitForm(){
        console.log(this.addFrom)
        if(this.addFrom.name === '' || this.addFrom.name === undefined){
          this.$message.error('商品名称不能为空')
          return
        }
        if(this.addFrom.goods_id === '' || this.addFrom.goods_id === undefined){
          this.$message.error('商品不能为空')
          return
        }
        if(this.addFrom.price === '' || this.addFrom.price === undefined){
          this.$message.error('商城售价不能为空')
          return
        }
        if(this.addFrom.cost_price === '' || this.addFrom.cost_price === undefined){
          this.$message.error('天津供货价不能为空')
          return
        }
        if(this.addFrom.market_price === '' || this.addFrom.market_price === undefined){
          this.$message.error('市场价不能为空')
          return
        }
        if(this.addFrom.goods_model === '' || this.addFrom.goods_model === undefined){
          this.$message.error('型号不能为空')
          return
        }
        if(this.addFrom.unit === '' || this.addFrom.unit === undefined){
          this.$message.error('销量单位不能为空')
          return
        }
        if(this.id !== undefined){
          this.getEdit()
        }else{
          this.getAdd()
        }
      },
      goBack() {
        this.$router.go(-1)
      }
    }
  }
</script>
<style scoped>
  page{
    position: relative;
  }
  .editor-btn{
    margin-top: 20px;
  }
</style>
