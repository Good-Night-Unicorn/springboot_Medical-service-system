<template>
  <div class="addEdit-block">
    <el-form
      class="detail-form-content"
      ref="ruleForm"
      :model="ruleForm"
      :rules="rules"
      label-width="80px"
	  :style="{backgroundColor:addEditForm.addEditBoxColor}"
    >
      <el-row>
                        <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="诊所名称" prop="zhensuomingcheng">
          <el-input v-model="ruleForm.zhensuomingcheng" 
              placeholder="诊所名称" clearable  :readonly="ro.zhensuomingcheng"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="诊所名称" prop="zhensuomingcheng">
              <el-input v-model="ruleForm.zhensuomingcheng" 
                placeholder="诊所名称" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'"  label="规模" prop="guimo">
          <el-select v-model="ruleForm.guimo" placeholder="请选择规模">
            <el-option
                v-for="(item,index) in guimoOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="规模" prop="guimo">
	      <el-input v-model="ruleForm.guimo"
                placeholder="规模" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'"  label="类型" prop="leixing">
          <el-select v-model="ruleForm.leixing" placeholder="请选择类型">
            <el-option
                v-for="(item,index) in leixingOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="类型" prop="leixing">
	      <el-input v-model="ruleForm.leixing"
                placeholder="类型" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="24">  
        <el-form-item class="upload" v-if="type!='info'" label="资格证书" prop="zigezhengshu">
          <file-upload
          tip="点击上传资格证书"
          action="file/upload"
          :limit="1"
          :multiple="true"
          :fileUrls="ruleForm.zigezhengshu?ruleForm.zigezhengshu:''"
          @change="zigezhengshuUploadChange"
          ></file-upload>
        </el-form-item>  
        <div v-else>
          <el-form-item v-if="ruleForm.zigezhengshu" label="资格证书" prop="zigezhengshu">
            <el-button type="text" size="small" @click="download(ruleForm.zigezhengshu)">下载</el-button>
          </el-form-item>
        </div>    
      </el-col>      
                                                                  <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="现有人数" prop="xianyourenshu">
          <el-input v-model="ruleForm.xianyourenshu" 
              placeholder="现有人数" clearable  :readonly="ro.xianyourenshu"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="现有人数" prop="xianyourenshu">
              <el-input v-model="ruleForm.xianyourenshu" 
                placeholder="现有人数" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="咨询电话" prop="zixundianhua">
          <el-input v-model="ruleForm.zixundianhua" 
              placeholder="咨询电话" clearable  :readonly="ro.zixundianhua"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="咨询电话" prop="zixundianhua">
              <el-input v-model="ruleForm.zixundianhua" 
                placeholder="咨询电话" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="账号" prop="zhanghao">
          <el-input v-model="ruleForm.zhanghao" 
              placeholder="账号" clearable  :readonly="ro.zhanghao"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="账号" prop="zhanghao">
              <el-input v-model="ruleForm.zhanghao" 
                placeholder="账号" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                    <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="姓名" prop="xingming">
          <el-input v-model="ruleForm.xingming" 
              placeholder="姓名" clearable  :readonly="ro.xingming"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="姓名" prop="xingming">
              <el-input v-model="ruleForm.xingming" 
                placeholder="姓名" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
                                                                                                                                                                                    <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="地址" prop="fulladdress">
          <el-input @click.native="openMapDiolag"  v-model="ruleForm.fulladdress" 
              placeholder="请选择地址"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" v-if="ruleForm.fulladdress" label="地址" prop="fulladdress">
              <el-input v-model="ruleForm.fulladdress" 
                placeholder="请选择地址" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
            </el-row>
                                                                                <el-row>
            <el-col :span="24">
              <el-form-item class="textarea" v-if="type!='info'" label="简介" prop="jianjie">
                <el-input
                  style="min-width: 200px; max-width: 600px;"
                  type="textarea"
                  :rows="8"
                  placeholder="简介"
                  v-model="ruleForm.jianjie" >
                </el-input>
              </el-form-item>
              <div v-else>
                <el-form-item v-if="ruleForm.jianjie" label="简介" prop="jianjie">
                    <span>{{ruleForm.jianjie}}</span>
                </el-form-item>
              </div>
            </el-col>
          </el-row>
                                                                                                                                                                                                                                                                                                                                                            <el-form-item class="btn">
                <el-button v-if="type!='info'" type="primary" class="btn-success" @click="onSubmit">提交</el-button>
        <el-button v-if="type!='info'" class="btn-close" @click="back()">取消</el-button>
        <el-button v-if="type=='info'" class="btn-close" @click="back()">返回</el-button>
      </el-form-item>
    </el-form>
    
        <el-dialog
      width="50%"
      title="坐标查询"
      :visible.sync="mapVisiable"
      append-to-body>
      <el-amap-search-box class="search-box" :on-search-result="onSearchResult" :search-option="searchOption" ></el-amap-search-box>
      <div class="amap-wrapper">
        <el-amap class="amap-box" :vid="'amap-vue'" 
        :center="center"
        :zoom="zoom"
        :events="events" >
          <el-amap-marker v-bind:key="marker" v-for="marker in markers" :position="marker" ></el-amap-marker>
        </el-amap>
      </div>
      <div>坐标：[{{ ruleForm.longitude }}, {{ ruleForm.latitude }}],地址：{{ruleForm.fulladdress}}</div>
    </el-dialog>
    
  </div>
</template>
<script>
// 数字，邮件，手机，url，身份证校验
import { isNumber,isIntNumer,isEmail,isPhone, isMobile,isURL,checkIdCard } from "@/utils/validate";
export default {
  data() {
    let self = this
    var validateIdCard = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!checkIdCard(value)) {
        callback(new Error("请输入正确的身份证号码"));
      } else {
        callback();
      }
    };
    var validateUrl = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isURL(value)) {
        callback(new Error("请输入正确的URL地址"));
      } else {
        callback();
      }
    };
    var validateMobile = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isMobile(value)) {
        callback(new Error("请输入正确的手机号码"));
      } else {
        callback();
      }
    };
    var validatePhone = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isPhone(value)) {
        callback(new Error("请输入正确的电话号码"));
      } else {
        callback();
      }
    };
    var validateEmail = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isEmail(value)) {
        callback(new Error("请输入正确的邮箱地址"));
      } else {
        callback();
      }
    };
    var validateNumber = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isNumber(value)) {
        callback(new Error("请输入数字"));
      } else {
        callback();
      }
    };
    var validateIntNumber = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isIntNumer(value)) {
        callback(new Error("请输入整数"));
      } else {
        callback();
      }
    };
    return {
	  addEditForm: {"btnSaveFontColor":"#fff","selectFontSize":"14px","btnCancelBorderColor":"#DCDFE6","inputBorderRadius":"4px","inputFontSize":"14px","textareaBgColor":"#fff","btnSaveFontSize":"14px","textareaBorderRadius":"4px","uploadBgColor":"#fff","textareaBorderStyle":"solid","btnCancelWidth":"88px","textareaHeight":"120px","dateBgColor":"#fff","btnSaveBorderRadius":"4px","uploadLableFontSize":"14px","textareaBorderWidth":"1px","inputLableColor":"#606266","addEditBoxColor":"#fff","dateIconFontSize":"14px","btnSaveBgColor":"rgba(36, 194, 205, 1)","uploadIconFontColor":"#8c939d","textareaBorderColor":"#DCDFE6","btnCancelBgColor":"#ecf5ff","selectLableColor":"#606266","btnSaveBorderStyle":"solid","dateBorderWidth":"1px","dateLableFontSize":"14px","dateBorderRadius":"4px","btnCancelBorderStyle":"solid","selectLableFontSize":"14px","selectBorderStyle":"solid","selectIconFontColor":"#C0C4CC","btnCancelHeight":"44px","inputHeight":"40px","btnCancelFontColor":"#606266","dateBorderColor":"#DCDFE6","dateIconFontColor":"#C0C4CC","uploadBorderStyle":"solid","dateBorderStyle":"solid","dateLableColor":"#606266","dateFontSize":"14px","inputBorderWidth":"1px","uploadIconFontSize":"28px","selectHeight":"40px","inputFontColor":"#606266","uploadHeight":"148px","textareaLableColor":"#606266","textareaLableFontSize":"14px","btnCancelFontSize":"14px","inputBorderStyle":"solid","btnCancelBorderRadius":"4px","inputBgColor":"#fff","inputLableFontSize":"14px","uploadLableColor":"#606266","uploadBorderRadius":"4px","btnSaveHeight":"44px","selectBgColor":"#fff","btnSaveWidth":"88px","selectIconFontSize":"14px","dateHeight":"40px","selectBorderColor":"#DCDFE6","inputBorderColor":"#DCDFE6","uploadBorderColor":"#DCDFE6","textareaFontColor":"#606266","selectBorderWidth":"1px","dateFontColor":"#606266","btnCancelBorderWidth":"1px","uploadBorderWidth":"1px","textareaFontSize":"14px","selectBorderRadius":"4px","selectFontColor":"#606266","btnSaveBorderColor":"#409EFF","btnSaveBorderWidth":"0px"},
      id: '',
      type: '',
      ro:{
	zhensuomingcheng : false,
	guimo : false,
	leixing : false,
	zigezhengshu : false,
	jianjie : false,
	xianyourenshu : false,
	zixundianhua : false,
	zhanghao : false,
	xingming : false,
	sfsh : false,
	shhf : false,
	longitude : false,
	latitude : false,
	fulladdress : false,
      },
            // 地图
      mapVisiable: false,
      zoom: 12,
      center: [116.410426, 39.934946],
      markers: [],
      searchOption: {
        citylimit: false
      },
      events: {
        click (e) {
          let { lng, lat } = e.lnglat
          self.ruleForm.longitude = lng
          self.ruleForm.latitude = lat
          // 这里通过高德 SDK 完成。
          /* eslint-disable */
          var geocoder = new AMap.Geocoder({
            radius: 1000,
            extensions: 'all'
          })
          geocoder.getAddress([lng, lat], function (status, result) {
            if (status === 'complete' && result.info === 'OK') {
              if (result && result.regeocode) {
                console.log(result)
                self.ruleForm.fulladdress = result.regeocode.formattedAddress
              }
            }
          })
        }
      },
            ruleForm: {
                	        zhensuomingcheng: '',
	                        	        guimo: '',
	                        	        leixing: '',
	                        	        zigezhengshu: '',
	                        	        jianjie: '',
	                        	        xianyourenshu: '',
	                        	        zixundianhua: '',
	                        	        zhanghao: '',
	                        	        xingming: '',
	                        	                        	        shhf: '',
	                        	        longitude: '',
	                        	        latitude: '',
	                        	        fulladdress: '',
	                      },
                                      guimoOptions: [],
                                leixingOptions: [],
                                                                                                                                                                              rules: {
                  zhensuomingcheng: [
                            { required: true, message: '诊所名称不能为空', trigger: 'blur' },
                                    	                                                              ],
                  guimo: [
                                    	                                                              ],
                  leixing: [
                                    	                                                              ],
                  zigezhengshu: [
                                    	                                                              ],
                  jianjie: [
                                    	                                                              ],
                  xianyourenshu: [
                                    	                                                              ],
                  zixundianhua: [
                                    	                                { validator: validatePhone, trigger: 'blur' },
                                                          ],
                  zhanghao: [
                                    	                                                              ],
                  xingming: [
                                    	                                                              ],
                  sfsh: [
                                    	                                                              ],
                  shhf: [
                                    	                                                              ],
                  longitude: [
                                                    { validator: validateNumber, trigger: 'blur' },
            	                                                              ],
                  latitude: [
                                                    { validator: validateNumber, trigger: 'blur' },
            	                                                              ],
                  fulladdress: [
                                    	                                                              ],
              }
    };
  },
  props: ["parent"],
  computed: {
                                                                                                                                                                              },
  created() {
	this.addEditStyleChange()
	this.addEditUploadStyleChange()
  },
  methods: {
        // 打开坐标定位窗口
    openMapDiolag () {
      this.mapVisiable = true
    },
    // 查询
    onSearchResult (pois) {
      let latSum = 0;
      let lngSum = 0;
      if (pois.length > 0) {
        pois.forEach(poi => {
          let {lng, lat} = poi;
          lngSum += lng;
          latSum += lat;
          this.markers.push([poi.lng, poi.lat]);
        });
        let center = {
          lng: lngSum / pois.length,
          lat: latSum / pois.length
        };
        this.center = [center.lng, center.lat];
      }
    },
        // 下载
    download(file){
      window.open(`${file}`)
    },
    // 初始化
    init(id,type) {
      if (id) {
        this.id = id;
        this.type = type;
      }
      if(this.type=='info'||this.type=='else'){
        this.info(id);
      }else if(this.type=='cross'){
        var obj = this.$storage.getObj('crossObj');
        for (var o in obj){
          	            if(o=='zhensuomingcheng'){
            this.ruleForm.zhensuomingcheng = obj[o];
	    this.ro.zhensuomingcheng = true;
            continue;
          }
	            	            if(o=='guimo'){
            this.ruleForm.guimo = obj[o];
	    this.ro.guimo = true;
            continue;
          }
	            	            if(o=='leixing'){
            this.ruleForm.leixing = obj[o];
	    this.ro.leixing = true;
            continue;
          }
	            	            if(o=='zigezhengshu'){
            this.ruleForm.zigezhengshu = obj[o];
	    this.ro.zigezhengshu = true;
            continue;
          }
	            	            if(o=='jianjie'){
            this.ruleForm.jianjie = obj[o];
	    this.ro.jianjie = true;
            continue;
          }
	            	            if(o=='xianyourenshu'){
            this.ruleForm.xianyourenshu = obj[o];
	    this.ro.xianyourenshu = true;
            continue;
          }
	            	            if(o=='zixundianhua'){
            this.ruleForm.zixundianhua = obj[o];
	    this.ro.zixundianhua = true;
            continue;
          }
	            	            if(o=='zhanghao'){
            this.ruleForm.zhanghao = obj[o];
	    this.ro.zhanghao = true;
            continue;
          }
	            	            if(o=='xingming'){
            this.ruleForm.xingming = obj[o];
	    this.ro.xingming = true;
            continue;
          }
	            	            	            	            if(o=='longitude'){
            this.ruleForm.longitude = obj[o];
	    this.ro.longitude = true;
            continue;
          }
	            	            if(o=='latitude'){
            this.ruleForm.latitude = obj[o];
	    this.ro.latitude = true;
            continue;
          }
	            	            if(o=='fulladdress'){
            this.ruleForm.fulladdress = obj[o];
	    this.ro.fulladdress = true;
            continue;
          }
	                    }
                                                                                                                                                                                                                                              }
            // 获取用户信息
      this.$http({
        url: `${this.$storage.get('sessionTable')}/session`,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
          var json = data.data;
                                                                                                                                                                                		if(json.zhanghao!=''&&json.zhanghao){
              		this.ruleForm.zhanghao = json.zhanghao
		}
                                  		if(json.xingming!=''&&json.xingming){
              		this.ruleForm.xingming = json.xingming
		}
                                                                                                                                            } else {
          this.$message.error(data.msg);
        }
      });
                                                            this.guimoOptions = "大型,中型,小型".split(',')
                                        this.leixingOptions = "国有,私立".split(',')
                                                                                                                                                                                                                                  },
                                                                                                                        // 多级联动参数
                                                                                                                                                        info(id) {
      this.$http({
        url: `xiangcunzhenshi/info/${id}`,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.ruleForm = data.data;
        } else {
          this.$message.error(data.msg);
        }
      });
    },
        // 提交
    onSubmit() {
                  // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                              // ${column.compare}
                                                                                                                                                                                                                                                                                                this.$refs["ruleForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: `xiangcunzhenshi/${!this.ruleForm.id ? "save" : "update"}`,
            method: "post",
            data: this.ruleForm
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$message({
                message: "操作成功",
                type: "success",
                duration: 1500,
                onClose: () => {
                  this.parent.showFlag = true;
                  this.parent.addOrUpdateFlag = false;
                  this.parent.xiangcunzhenshiCrossAddOrUpdateFlag = false;
                  this.parent.search();
                  this.parent.contentStyleChange();
                }
              });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    },
    // 获取uuid
    getUUID () {
      return new Date().getTime();
    },
    // 返回
    back() {
      this.parent.showFlag = true;
      this.parent.addOrUpdateFlag = false;
      this.parent.xiangcunzhenshiCrossAddOrUpdateFlag = false;
      this.parent.contentStyleChange();
    },
                                                            zigezhengshuUploadChange(fileUrls) {
                this.ruleForm.zigezhengshu = fileUrls;
				this.addEditUploadStyleChange()
            },
                                                                                                                                    	addEditStyleChange() {
	  this.$nextTick(()=>{
	    // input
	    document.querySelectorAll('.addEdit-block .input .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.inputHeight
	      el.style.color = this.addEditForm.inputFontColor
	      el.style.fontSize = this.addEditForm.inputFontSize
	      el.style.borderWidth = this.addEditForm.inputBorderWidth
	      el.style.borderStyle = this.addEditForm.inputBorderStyle
	      el.style.borderColor = this.addEditForm.inputBorderColor
	      el.style.borderRadius = this.addEditForm.inputBorderRadius
	      el.style.backgroundColor = this.addEditForm.inputBgColor
	    })
	    document.querySelectorAll('.addEdit-block .input .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.inputHeight
	      el.style.color = this.addEditForm.inputLableColor
	      el.style.fontSize = this.addEditForm.inputLableFontSize
	    })
	    // select
	    document.querySelectorAll('.addEdit-block .select .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.selectHeight
	      el.style.color = this.addEditForm.selectFontColor
	      el.style.fontSize = this.addEditForm.selectFontSize
	      el.style.borderWidth = this.addEditForm.selectBorderWidth
	      el.style.borderStyle = this.addEditForm.selectBorderStyle
	      el.style.borderColor = this.addEditForm.selectBorderColor
	      el.style.borderRadius = this.addEditForm.selectBorderRadius
	      el.style.backgroundColor = this.addEditForm.selectBgColor
	    })
	    document.querySelectorAll('.addEdit-block .select .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.selectHeight
	      el.style.color = this.addEditForm.selectLableColor
	      el.style.fontSize = this.addEditForm.selectLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .select .el-select__caret').forEach(el=>{
	      el.style.color = this.addEditForm.selectIconFontColor
	      el.style.fontSize = this.addEditForm.selectIconFontSize
	    })
	    // date
	    document.querySelectorAll('.addEdit-block .date .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.dateHeight
	      el.style.color = this.addEditForm.dateFontColor
	      el.style.fontSize = this.addEditForm.dateFontSize
	      el.style.borderWidth = this.addEditForm.dateBorderWidth
	      el.style.borderStyle = this.addEditForm.dateBorderStyle
	      el.style.borderColor = this.addEditForm.dateBorderColor
	      el.style.borderRadius = this.addEditForm.dateBorderRadius
	      el.style.backgroundColor = this.addEditForm.dateBgColor
	    })
	    document.querySelectorAll('.addEdit-block .date .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.dateHeight
	      el.style.color = this.addEditForm.dateLableColor
	      el.style.fontSize = this.addEditForm.dateLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .date .el-input__icon').forEach(el=>{
	      el.style.color = this.addEditForm.dateIconFontColor
	      el.style.fontSize = this.addEditForm.dateIconFontSize
	      el.style.lineHeight = this.addEditForm.dateHeight
	    })
	    // upload
	    let iconLineHeight = parseInt(this.addEditForm.uploadHeight) - parseInt(this.addEditForm.uploadBorderWidth) * 2 + 'px'
	    document.querySelectorAll('.addEdit-block .upload .el-upload--picture-card').forEach(el=>{
	      el.style.width = this.addEditForm.uploadHeight
	      el.style.height = this.addEditForm.uploadHeight
	      el.style.borderWidth = this.addEditForm.uploadBorderWidth
	      el.style.borderStyle = this.addEditForm.uploadBorderStyle
	      el.style.borderColor = this.addEditForm.uploadBorderColor
	      el.style.borderRadius = this.addEditForm.uploadBorderRadius
	      el.style.backgroundColor = this.addEditForm.uploadBgColor
	    })
	    document.querySelectorAll('.addEdit-block .upload .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.uploadHeight
	      el.style.color = this.addEditForm.uploadLableColor
	      el.style.fontSize = this.addEditForm.uploadLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .upload .el-icon-plus').forEach(el=>{
	      el.style.color = this.addEditForm.uploadIconFontColor
	      el.style.fontSize = this.addEditForm.uploadIconFontSize
	      el.style.lineHeight = iconLineHeight
	      el.style.display = 'block'
	    })
	    // 多文本输入框
	    document.querySelectorAll('.addEdit-block .textarea .el-textarea__inner').forEach(el=>{
	      el.style.height = this.addEditForm.textareaHeight
	      el.style.color = this.addEditForm.textareaFontColor
	      el.style.fontSize = this.addEditForm.textareaFontSize
	      el.style.borderWidth = this.addEditForm.textareaBorderWidth
	      el.style.borderStyle = this.addEditForm.textareaBorderStyle
	      el.style.borderColor = this.addEditForm.textareaBorderColor
	      el.style.borderRadius = this.addEditForm.textareaBorderRadius
	      el.style.backgroundColor = this.addEditForm.textareaBgColor
	    })
	    document.querySelectorAll('.addEdit-block .textarea .el-form-item__label').forEach(el=>{
	      // el.style.lineHeight = this.addEditForm.textareaHeight
	      el.style.color = this.addEditForm.textareaLableColor
	      el.style.fontSize = this.addEditForm.textareaLableFontSize
	    })
	    // 保存
	    document.querySelectorAll('.addEdit-block .btn .btn-success').forEach(el=>{
	      el.style.width = this.addEditForm.btnSaveWidth
	      el.style.height = this.addEditForm.btnSaveHeight
	      el.style.color = this.addEditForm.btnSaveFontColor
	      el.style.fontSize = this.addEditForm.btnSaveFontSize
	      el.style.borderWidth = this.addEditForm.btnSaveBorderWidth
	      el.style.borderStyle = this.addEditForm.btnSaveBorderStyle
	      el.style.borderColor = this.addEditForm.btnSaveBorderColor
	      el.style.borderRadius = this.addEditForm.btnSaveBorderRadius
	      el.style.backgroundColor = this.addEditForm.btnSaveBgColor
	    })
	    // 返回
	    document.querySelectorAll('.addEdit-block .btn .btn-close').forEach(el=>{
	      el.style.width = this.addEditForm.btnCancelWidth
	      el.style.height = this.addEditForm.btnCancelHeight
	      el.style.color = this.addEditForm.btnCancelFontColor
	      el.style.fontSize = this.addEditForm.btnCancelFontSize
	      el.style.borderWidth = this.addEditForm.btnCancelBorderWidth
	      el.style.borderStyle = this.addEditForm.btnCancelBorderStyle
	      el.style.borderColor = this.addEditForm.btnCancelBorderColor
	      el.style.borderRadius = this.addEditForm.btnCancelBorderRadius
	      el.style.backgroundColor = this.addEditForm.btnCancelBgColor
	    })
	  })
	},
	addEditUploadStyleChange() {
		this.$nextTick(()=>{
		  document.querySelectorAll('.addEdit-block .upload .el-upload-list--picture-card .el-upload-list__item').forEach(el=>{
			el.style.width = this.addEditForm.uploadHeight
			el.style.height = this.addEditForm.uploadHeight
			el.style.borderWidth = this.addEditForm.uploadBorderWidth
			el.style.borderStyle = this.addEditForm.uploadBorderStyle
			el.style.borderColor = this.addEditForm.uploadBorderColor
			el.style.borderRadius = this.addEditForm.uploadBorderRadius
			el.style.backgroundColor = this.addEditForm.uploadBgColor
		  })
	  })
	},
  }
};
</script>
<style lang="scss">
.editor{
  height: 500px;
  
  & /deep/ .ql-container {
	  height: 310px;
  }
}
.amap-wrapper {
  width: 100%;
  height: 500px;
}
.search-box {
  position: absolute;
}
.addEdit-block {
	margin: -10px;
}
.detail-form-content {
	padding: 12px;
}
.btn .el-button {
  padding: 0;
}
</style>
