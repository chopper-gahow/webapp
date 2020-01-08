<template>
  <briup-fulllayout title="修改地址">
    <div>
      {{form}}
      <van-cell-group>
        <van-field v-model="form.telephone" placeholder="手机号" />
      </van-cell-group>
      <van-cell-group>
        <van-field v-model="form.province" placeholder="省" />
      </van-cell-group>
       <van-cell-group>
        <van-field v-model="form.city" placeholder="市" />
      </van-cell-group>
       <van-cell-group>
        <van-field v-model="form.area" placeholder="区" />
      </van-cell-group>
      <van-cell-group>
        <van-field v-model="form.address" placeholder="详细地址" />
      </van-cell-group>

      <van-button block type="primary" @click="updateHandler">保存</van-button>

    </div>
  </briup-fulllayout>
</template>
<script>
import {post} from '../../../http/axios'
import { mapState } from 'vuex';
import { Toast } from 'vant';
export default {
  data(){
    return {
      form:{}
    }
  },
  computed:{
    ...mapState('user',['info'])
  },
  methods:{
    updateHandler(){
      let url = "/address/saveOrUpdate?id="+this.$route.query.id
      this.form.customerId = this.info.id;
      post(url,this.form).then((response)=>{
        // 返回上一个页面
        this.$router.go(-1);
        // 轻提示，提示成功消息
        this.$toast.success(response.message)
      })
    }
  }
}
</script>