<template>
  <div id="C_content">
    <div class="C_container">
      <div class="C_title"><span class="Title_left"></span>标准制定企业</div>
      <div class="el-tab">
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane label="国家标准" name="first">
            <div class="ind-title">
              <p>
                <i class="icon icon-tips"></i>
                <span>国家标准列表</span> 标准制定企业共
                <span id="Tag">{{ total }}</span> 家
              </p>
            </div>
            <div class="form-wrapper">
              <form class="form-inline" role="form">
                <div class="form-group">
                  <span class="control-label">年份 ：</span>
                  <el-select v-model="faburq" placeholder="请选择年份">
                    <el-option label="选择所有" value></el-option>
                    <el-option
                      v-for="item in years"
                      :key="item.faburq"
                      :label="item.faburq"
                      :value="item.faburq"
                    ></el-option>
                  </el-select>
                </div>

                <div class="form-group">
                  <div class="ui-input ui-input-search PuKey">
                    <i class="el-icon-search"></i>
                    <input
                      class="key"
                      v-model="gongsiname"
                      placeholder="请输入标准起草单位"
                      type="text"
                      autocomplete="off"
                    />
                  </div>
                </div>
                <!-- <div class="form-group">
                  <button
                    class="btn btn-query btn-action"
                    @click="search()"
                    type="button"
                    role="button"
                  >
                    <span class="chaxun">查询</span>
                    <i class="icon-loading icon-loading-white a-spin"></i>
                  </button>
                </div> -->
                <el-button @click="search()" type="primary">查询</el-button>
              </form>
            </div>
            <div class="query-result">
              <div class="table-wrapper">
                <el-table stripe :data="tableData" style="width: 100%">
                  <el-table-column prop="gongsiname" label="标准起草单位">
                    <template slot-scope="scope">
                      <router-link
                        target="_blank"
                        tag="a"
                        style="color:#606266;text-decoration:none;"
                        :to="{ path:'/CompanyDetails', query: { name: Base64.encode(scope.row.gongsiname) }}"
                      >{{ scope.row.gongsiname }}</router-link>
                    </template>
                  </el-table-column>
                  <el-table-column prop="gongsilx" label="公司类型"></el-table-column>
                  <el-table-column prop="zhuczb" label="注册资本(万元)"></el-table-column>
                  <el-table-column prop="zhuguanbm" label="主管单位"></el-table-column>
                  <el-table-column prop="biaozhunmc" label="标准名称"></el-table-column>
                  <el-table-column prop="biaozhunh" label="标准编号"></el-table-column>
                  <el-table-column prop="faburq" label="发布日期" width="150"></el-table-column>
                  <el-table-column prop label="详情" width="100">
                      <template slot-scope="scope">
                        <el-popover trigger="hover" placement="left" width="500">
                          <p class="fontSize20"> <b>起草单位</b>:  {{ scope.row.qicaodw }}</p><br>
                          <p> <b>归口单位</b>:  {{ scope.row.guikoudw }}</p><br>
                          <p> <b>中国标准分类号</b>:  {{ scope.row.zhongguobz }}</p><br>
                          <p> <b>采标情况</b>:  {{ scope.row.caibiaoqk }}</p><br>
                          <p> <b>起草人</b>: {{ scope.row.qicaoren }}</p><br>
                          <p><b>国际标准分类号</b>: {{ scope.row.guojibiaozflh }}</p>
                          <div slot="reference" class="name-wrapper">
                            <el-tag size="medium">详情</el-tag>
                          </div>
                        </el-popover>
                      </template>
                  </el-table-column>
                </el-table>
              </div>
            </div>
            <!-- 分页dom start -->
                    <div id="Pagination">
                        <el-pagination layout="prev, pager, next" prev-text="上一页" next-text="下一页" @current-change="handleCurrentChange"  :page-size="20" :current-page="page"></el-pagination>
                        <el-button size="small" :disabled="suibian" class="paginationsy" @click="paginationsy">首页</el-button>
                    </div>
              <!-- 分页dom end -->
          </el-tab-pane>
          <el-tab-pane label="地方标准" name="second">
            <div class="ind-title">
              <p>
                <i class="icon icon-tips"></i>
                <span>地方标准列表</span> 标准制定企业共
                <span id="Tag">{{ total }}</span> 家
              </p>
            </div>
            <div class="form-wrapper">
              <form class="form-inline" role="form">
                <div class="form-group">
                  <span class="control-label">年份 ：</span>
                  <el-select v-model="faburq" placeholder="请选择年份">
                    <el-option label="选择所有" value></el-option>
                    <el-option
                      v-for="item in years"
                      :key="item.faburq"
                      :label="item.faburq"
                      :value="item.faburq"
                    ></el-option>
                  </el-select>
                </div>

                <div class="form-group">
                  <div class="ui-input ui-input-search PuKey">
                    <i class="el-icon-search"></i>
                    <input
                      class="key"
                      v-model="gongsiname"
                      placeholder="请输入标准起草单位"
                      type="text"
                      autocomplete="off"
                    />
                  </div>
                </div>
                <!-- <div class="form-group">
                  <button
                    class="btn btn-query btn-action"
                    @click="search()"
                    type="button"
                    role="button"
                  >
                    <span class="chaxun">查询</span>
                    <i class="icon-loading icon-loading-white a-spin"></i>
                  </button>
                </div> -->
                <el-button @click="tablelist()" type="primary">查询</el-button>
              </form>
            </div>
            <div class="query-result">
              <div class="table-wrapper">
                <el-table stripe :data="tableData" style="width: 100%">
                  <el-table-column prop="gongsiname" label="标准起草单位">
                    <template slot-scope="scope">
                      <router-link
                        target="_blank"
                        tag="a"
                        style="color:#606266;text-decoration:none;"
                        :to="{ path:'/CompanyDetails', query: { name: Base64.encode(scope.row.gongsiname) }}"
                      >{{ scope.row.gongsiname }}</router-link>
                    </template>
                  </el-table-column>
                  <el-table-column prop="gongsilx" label="公司类型"></el-table-column>
                  <el-table-column prop="zhuczb" label="注册资本(万元)"></el-table-column>
                  <el-table-column prop="zhuguanbm" label="主管单位"></el-table-column>
                  <el-table-column prop="biaozhunmc" label="标准名称"></el-table-column>
                  <el-table-column prop="biaozhunh" label="标准编号"></el-table-column>
                  <el-table-column prop="faburq" label="发布日期"></el-table-column>
                  <el-table-column prop label="详情" width="100">
                      <template slot-scope="scope">
                        <el-popover trigger="hover" placement="left" width="500">
                          <p> <b>起草单位</b>:  {{ scope.row.qicaodw }}</p><br>
                          <p> <b>归口单位</b>:  {{ scope.row.guikoudw }}</p><br>
                          <p> <b>中国标准分类号</b>:  {{ scope.row.zhongguobz }}</p><br>
                          <p> <b>行业分类</b>:  {{ scope.row.hangyefl }}</p><br>
                          <p> <b>起草人</b>: {{ scope.row.qicaoren }}</p><br>
                          <p><b>国际标准分类号</b>: {{ scope.row.guojibiaozflh }}</p>
                          <div slot="reference" class="name-wrapper">
                            <el-tag size="medium">详情</el-tag>
                          </div>
                        </el-popover>
                      </template>
                  </el-table-column>
                </el-table>
              </div>
            </div>
            <!-- 分页dom start -->
                    <div id="Pagination">
                        <el-pagination layout="prev, pager, next" prev-text="上一页" next-text="下一页" @current-change="handleCurrentChange"  :page-size="20" :current-page="page"></el-pagination>
                        <el-button size="small" :disabled="suibian" class="paginationsy" @click="paginationsy">首页</el-button>
                    </div>
              <!-- 分页dom end -->
          </el-tab-pane>
          <el-tab-pane label="行业标准" name="third">
            <div class="ind-title">
              <p>
                <i class="icon icon-tips"></i>
                <span>行业标准列表</span> 标准制定企业共
                <span id="Tag">{{ total }}</span>
                家
              </p>
            </div>
            <div class="form-wrapper">
              <form class="form-inline" role="form">
                <div class="form-group">
                  <span class="control-label">年份 ：</span>
                  <el-select v-model="faburq" placeholder="请选择年份">
                    <el-option label="选择所有" value></el-option>
                    <el-option
                      v-for="item in years"
                      :key="item.faburq"
                      :label="item.faburq"
                      :value="item.faburq"
                    ></el-option>
                  </el-select>
                </div>

                <div class="form-group">
                  <div class="ui-input ui-input-search PuKey">
                    <i class="el-icon-search"></i>
                    <input
                      class="key"
                      v-model="gongsiname"
                      placeholder="请输入标准起草单位"
                      type="text"
                      autocomplete="off"
                    />
                  </div>
                </div>
                <!-- <div class="form-group">
                  <button
                    class="btn btn-query btn-action"
                    @click="search()"
                    type="button"
                    role="button"
                  >
                    <span class="chaxun">查询</span>
                    <i class="icon-loading icon-loading-white a-spin"></i>
                  </button>
                </div> -->
                <el-button @click="tablelist()" type="primary">查询</el-button>
              </form>
            </div>
            <div class="query-result">
              <div class="table-wrapper">
                <el-table stripe :data="tableData" style="width: 100%">
                  <el-table-column prop="gongsiname" label="标准起草单位">
                    <template slot-scope="scope">
                      <router-link
                        target="_blank"
                        tag="a"
                        style="color:#606266;text-decoration:none;"
                        :to="{ path:'/CompanyDetails', query: { name: Base64.encode(scope.row.gongsiname) }}"
                      >{{ scope.row.gongsiname }}</router-link>
                    </template>
                  </el-table-column>
                  <el-table-column prop="gongsilx" label="公司类型"></el-table-column>
                  <el-table-column prop="zhuczb" label="注册资本(万元)"></el-table-column>
                  <el-table-column prop="zhuguanbm" label="主管单位"></el-table-column>
                  <el-table-column prop="biaozhunmc" label="标准名称"></el-table-column>
                  <el-table-column prop="biaozhunh" label="标准编号"></el-table-column>
                  <el-table-column prop="faburq" label="发布日期"></el-table-column>
                  <el-table-column prop label="详情" width="100">
                      <template slot-scope="scope">
                        <el-popover trigger="hover" placement="left" width="500">
                          <p> <b>起草单位</b>:  {{ scope.row.qicaodw }}</p><br>
                          <p> <b>归口单位</b>:  {{ scope.row.guikoudw }}</p><br>
                          <p> <b>中国标准分类号</b>:  {{ scope.row.zhongguobz }}</p><br>
                          <p> <b>行业分类</b>:  {{ scope.row.hangyefl }}</p><br>
                          <p> <b>起草人</b>: {{ scope.row.qicaoren }}</p><br>
                          <p><b>国际标准分类号</b>: {{ scope.row.guojibiaozflh }}</p>
                          <div slot="reference" class="name-wrapper">
                            <el-tag size="medium">详情</el-tag>
                          </div>
                        </el-popover>
                      </template>
                  </el-table-column>
                </el-table>
              </div>
            </div>
            <!-- 分页dom start -->
                    <div id="Pagination">
                        <el-pagination layout="prev, pager, next" prev-text="上一页" next-text="下一页" @current-change="handleCurrentChange"  :page-size="20" :current-page="page"></el-pagination>
                        <el-button size="small" :disabled="suibian" class="paginationsy" @click="paginationsy">首页</el-button>
                    </div>
              <!-- 分页dom end -->
          </el-tab-pane>
          <el-tab-pane label="企业标准" name="fourth">
            <div class="ind-title">
              <p>
                <i class="icon icon-tips"></i>
                <span>企业标准列表</span> 标准制定企业共
                <span id="Tag">{{ total }}</span> 家
              </p>
            </div>
            <div class="form-wrapper">
              <form class="form-inline" role="form">
                <div class="form-group">
                  <span class="control-label">年份 ：</span>
                  <el-select v-model="faburq" placeholder="请选择年份">
                    <el-option label="选择所有" value></el-option>
                    <el-option
                      v-for="item in years"
                      :key="item.faburq"
                      :label="item.faburq"
                      :value="item.faburq"
                    ></el-option>
                  </el-select>
                </div>

                <div class="form-group">
                  <div class="ui-input ui-input-search PuKey">
                    <i class="el-icon-search"></i>
                    <input
                      class="key"
                      v-model="gongsiname"
                      placeholder="请输入标准起草单位"
                      type="text"
                      autocomplete="off"
                    />
                  </div>
                </div>
                <!-- <div class="form-group">
                  <button
                    class="btn btn-query btn-action"
                    @click="search()"
                    type="button"
                    role="button"
                  >
                    <span class="chaxun">查询</span>
                    <i class="icon-loading icon-loading-white a-spin"></i>
                  </button>
                </div> -->
                <el-button @click="tablelist()" type="primary">查询</el-button>
              </form>
            </div>
            <div class="query-result">
              <div class="table-wrapper">
                <el-table stripe :data="tableData" style="width: 100%">
                  <el-table-column prop="gongsiname" label="标准起草单位">
                    <template slot-scope="scope">
                      <router-link
                        target="_blank"
                        tag="a"
                        style="color:#606266;text-decoration:none;"
                        :to="{ path:'/CompanyDetails', query: { name: Base64.encode(scope.row.gongsiname) }}"
                      >{{ scope.row.gongsiname }}</router-link>
                    </template>
                  </el-table-column>
                  <el-table-column prop="gongsilx" label="公司类型"></el-table-column>
                  <el-table-column prop="zhuczb" label="注册资本(万元)"></el-table-column>
                  <el-table-column prop="biaozhunmc" label="标准名称"></el-table-column>
                  <el-table-column prop="biaozhunh" label="标准编号"></el-table-column>
                  <el-table-column prop="faburq" label="发布日期"></el-table-column>
                  <!-- <el-table-column prop="" label="详情"><a href="#" style="color:#c03532">详情</a>  </el-table-column> -->
                  <!-- <el-table-column prop label="详情" width="100">
                      <template slot-scope="scope">
                        <el-popover trigger="hover" placement="left" width="500">
                          <p> <b>起草单位</b>:  {{ scope.row.qicaodw }}</p><br>
                          <p> <b>范围</b> : {{ scope.row.fanwei }}</p><br>
                          <p> <b>起草人</b>: {{ scope.row.qicaoren }}</p><br>
                          <p><b>国际标准分类号</b>: {{ scope.row.guojibiaozflh }}</p>
                          <div slot="reference" class="name-wrapper">
                            <el-tag size="medium">详情</el-tag>
                          </div>
                        </el-popover>
                      </template>
                  </el-table-column> -->
                </el-table>
              </div>
            </div>
             <!-- 分页dom start -->
                    <div id="Pagination">
                        <el-pagination layout="prev, pager, next" prev-text="上一页" next-text="下一页" @current-change="handleCurrentChange"  :page-size="20" :current-page="page"></el-pagination>
                        <el-button size="small" :disabled="suibian" class="paginationsy" @click="paginationsy">首页</el-button>
                    </div>
              <!-- 分页dom end -->
          </el-tab-pane>
          <el-tab-pane label="团体标准" name="fifth">
            <div class="ind-title">
              <p>
                <i class="icon icon-tips"></i>
                <span>团体标准列表</span> 标准制定企业共
                <span id="Tag">{{ total }}</span> 家
              </p>
            </div>
            <div class="form-wrapper">
              <form class="form-inline" role="form">
                <div class="form-group">
                  <span class="control-label">年份 ：</span>
                  <el-select v-model="faburq" placeholder="请选择年份">
                    <el-option label="选择所有" value></el-option>
                    <el-option
                      v-for="item in years"
                      :key="item.faburq"
                      :label="item.faburq"
                      :value="item.faburq"
                      :current-page="page"
                    ></el-option>
                  </el-select>
                </div>

                <div class="form-group">
                  <div class="ui-input ui-input-search PuKey">
                    <i class="el-icon-search"></i>
                    <input
                      class="key"
                      v-model="gongsiname"
                      placeholder="请输入标准起草单位"
                      type="text"
                      autocomplete="off"
                    />
                  </div>
                </div>
                <!-- <div class="form-group">
                  <button
                    class="btn btn-query btn-action"
                    @click="search()"
                    type="button"
                    role="button"
                  >
                    <span class="chaxun">查询</span>
                    <i class="icon-loading icon-loading-white a-spin"></i>
                  </button>
                </div> -->
                <el-button @click="tablelist()" type="primary">查询</el-button>
              </form>
            </div>
            <div class="query-result">
              <div class="table-wrapper">
                <el-table stripe :data="tableData" style="width: 100%">
                  <el-table-column prop="gongsiname" label="标准起草单位">
                    <template slot-scope="scope">
                      <router-link
                        target="_blank"
                        tag="a"
                        style="color:#606266;text-decoration:none;"
                        :to="{ path:'/CompanyDetails', query: { name: Base64.encode(scope.row.gongsiname) }}"
                      >{{ scope.row.gongsiname }}</router-link>
                    </template>
                  </el-table-column>
                  <el-table-column prop="gongsilx" label="公司类型"></el-table-column>
                  <el-table-column prop="biaozhunmc" label="标准名称"></el-table-column>
                  <el-table-column prop="zhuczb" label="注册资本(万元)"></el-table-column>
                  <el-table-column prop="faburq" width="200" label="发布日期"></el-table-column>
                  <el-table-column prop label="详情" width="100">
                      <template slot-scope="scope">
                        <el-popover trigger="hover" placement="left" width="500">
                          <p> <b>起草单位</b>:  {{ scope.row.qicaodw }}</p><br>
                          <p> <b>范围</b> : {{ scope.row.fanwei }}</p><br>
                          <p> <b>起草人</b>: {{ scope.row.qicaoren }}</p><br>
                          <p><b>国际标准分类号</b>: {{ scope.row.guojibiaozflh }}</p>
                          <div slot="reference" class="name-wrapper">
                            <el-tag size="medium">详情</el-tag>
                          </div>
                        </el-popover>
                      </template>
                  </el-table-column>
                </el-table>
              </div>
            </div>
            <!-- 分页dom start -->
                    <div id="Pagination">
                        <el-pagination layout="prev, pager, next" prev-text="上一页" next-text="下一页" @current-change="handleCurrentChange"  :page-size="20" :current-page="page"></el-pagination>
                        <el-button size="small" :disabled="suibian" class="paginationsy" @click="paginationsy">首页</el-button>
                    </div>
              <!-- 分页dom end -->
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gongsiname: "",
      value: "",
      activeName: "first",
      options: [],
      years: [],
      faburq: "",
      tableData: [],
      ziduanqufen: "a",
      total: 0,
      page:1,
      suibian:true    //分页变量3
    };
  },
  mounted() {
    var self = this;
    self.select();
    self.tableList();
  },
   watch:{
    page(val) {
      var self=this
            if(val == 1){
                self.suibian=true
            }
        }
  },
  //end
  created() {},
  methods: {
     // 分页--回到首页按钮  start
        paginationsy() {
            if(this.page === 1) {

            }else{
                // this.page = 1
                this.handleCurrentChange(1)
            }
        },
        // 分页--回到首页按钮  end
    handleCurrentChange(val) {
      var self = this;
      // console.log(`当前页: ${val}`);
      self.page = val;
            var cot =  parseInt(self.total/20)+1
            self.suibian=false  //是否禁用首页按钮
      // console.log(self.page);
      self.tableList(val, 20);
    },
    handleClick(tab, event) {
      var self = this;
      self.page=1
      // console.log(tab, event);
      if (tab.index == 1) {
        self.gongsiname = "";
        self.tableData = [];
        self.faburq = "";
        self.ziduanqufen = "b";
        self.tableList();
        self.select();
      } else if (tab.index == 0) {
        self.faburq = "";
        self.gongsiname = "";
        self.tableData = [];
        self.ziduanqufen = "a";
        self.tableList();
        self.select();
      } else if (tab.index == 2) {
        self.faburq = "";
        self.gongsiname = "";
        self.tableData = [];
        self.ziduanqufen = "c";
        self.tableList();
        self.select();
      } else if (tab.index == 3) {
        self.gongsiname = "";
        self.faburq = "";
        self.tableData = [];
        self.ziduanqufen = "d";
        self.tableList();
        self.select();
      } else if (tab.index == 4) {
        self.faburq = "";
        self.gongsiname = "";
        self.tableData = [];
        self.ziduanqufen = "e";
        self.tableList();
        self.select();
      }
    },
    select() {
      var self = this;
      let params = {
        ziduanqufen: self.ziduanqufen
      };
      this.axios({
        url: this.api.standardseSelect,
        data: this.$qs.stringify(params),
        method: "post",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded"
        }
      }).then(res => {
        // console.log(JSON.stringify(res.data.data));
        self.years = res.data.data;
      });
    },
     search(){
      var self=this
      self.page=1
      self.tableList()
    },


    tableList() {
      var self = this;
      var right = document.getElementsByClassName('btn-next')
right[0].disabled=""
      let params = {
        page: self.page,
        limit: 20,
        ziduanqufen: self.ziduanqufen,
        faburq: self.faburq,
        gongsiname: self.gongsiname
      };
      this.axios({
        url: this.api.standardseList,
        method: "post",
        data: this.$qs.stringify(params),
        headers: {
          "Content-Type": "application/x-www-form-urlencoded"
        }
      }).then(res => {
        // console.log(JSON.stringify(res.data.data));
        self.tableData = res.data.data;
        self.total = res.data.count;
         // 分页--下一页disabled
                var cot =  parseInt(self.total/20)+1
                if(cot <= self.page){
                    right[0].disabled="disabled"
                }else if(self.page==1){
                    self.suibian=true
                }
                // 分页--下一页disabled
      });
    }
  }
};
</script>

<style lang="scss" >
@import "../../assets/css/Public_style.scss";
@import "../../styles/css/Techindustry.scss";

</style>