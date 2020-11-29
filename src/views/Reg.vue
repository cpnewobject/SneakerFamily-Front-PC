<template>
  <div class="layui-container fly-marginTop">
    <div class="fly-panel fly-panel-user" pad20>
      <div class="layui-tab layui-tab-brief" lay-filter="user">
        <ul class="layui-tab-title">
          <li>
            <router-link :to="{ name: 'login' }">登录</router-link>
          </li>
          <li class="layui-this">注册</li>
        </ul>
        <div
          class="layui-form layui-tab-content"
          id="LAY_ucm"
          style="padding: 20px 0;"
        >
          <div class="layui-tab-item layui-show">
            <div class="layui-form layui-form-pane">
              <form method="post">
                <div class="layui-form-item">
                  <label for="L_email" class="layui-form-label">邮箱</label>
                  <div class="layui-input-inline">
                    <input
                      type="text"
                      name="username"
                      v-model="username"
                      v-validate="'required|email'"
                      placeholder="请输入用户名"
                      autocomplete="off"
                      class="layui-input"
                    />
                  </div>
                  <div class="layui-form-mid layui-word-aux">
                    将会成为您唯一的登入名
                  </div>
                </div>
                <div class="error-item">
                  <span class="error">{{
                    errors.first('username')
                  }}</span>
                </div>
                <div class="layui-form-item">
                  <label for="L_username" class="layui-form-label">昵称</label>
                  <div class="layui-input-inline">
                    <input
                      type="text"
                      name="nickname"
                      v-model="nickname"
                      v-validate="'required|min:4'"
                      autocomplete="off"
                      placeholder="请输入昵称"
                      class="layui-input"
                    />
                  </div>
                </div>
                <div class="error-item">
                  <span class="error">{{
                    errors.first('nickname')
                  }}</span>
                </div>
                <div class="layui-form-item">
                  <label for="L_pass" class="layui-form-label">密码</label>
                  <div class="layui-input-inline">
                    <input
                      type="password"
                      name="password"
                      v-model="password"
                      v-validate="'required|min:6'"
                      placeholder="请输入密码"
                      autocomplete="off"
                      class="layui-input"
                    />
                  </div>
                  <div class="layui-form-mid layui-word-aux">6到16个字符</div>
                </div>
                <div class="error-item">
                  <span class="error">{{
                    errors.first('password')
                  }}</span>
                </div>
                <div class="layui-form-item">
                  <label for="L_repass" class="layui-form-label"
                    >确认密码</label
                  >
                  <div class="layui-input-inline">
                    <input
                      type="password"
                      name="c_password"
                      v-model="c_password"
                      v-validate="'required|min:6'"
                      placeholder="请输入确认密码"
                      autocomplete="off"
                      class="layui-input"
                    />
                  </div>
                </div>
                <div class="error-item">
                  <span class="error">{{
                    errors.first('c_password')
                  }}</span>
                </div>
                <div class="layui-form-item">
                  <div class="layui-row">
                    <label for="L_vercode" class="layui-form-label"
                      >验证码</label
                    >
                    <div class="layui-input-inline">
                      <input
                        type="text"
                        name="code"
                        v-model="code"
                        v-validate="'required|length:4'"
                        placeholder="请输入验证码"
                        autocomplete="off"
                        class="layui-input"
                      />
                    </div>
                    <div>
                      <span class="svg" v-html="svg" @click="_getCaptcha()"></span>
                    </div>
                    <div>
                      <span class="error layui-form-mid">{{
                        errors.first('code')
                      }}</span>
                    </div>
                  </div>
                </div>
                <div class="layui-form-item">
                  <button class="layui-btn" lay-filter="*" lay-submit>
                    立即注册
                  </button>
                </div>
                <div class="layui-form-item fly-form-app">
                  <span>或者直接使用社交账号快捷注册</span>
                  <a
                    href=""
                    onclick="layer.msg('正在通过QQ登入', {icon:16, shade: 0.1, time:0})"
                    class="iconfont icon-qq"
                    title="QQ登入"
                  ></a>
                  <a
                    href=""
                    onclick="layer.msg('正在通过微博登入', {icon:16, shade: 0.1, time:0})"
                    class="iconfont icon-weibo"
                    title="微博登入"
                  ></a>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getCode } from '@/api/login'
export default {
  name: 'reg',
  data () {
    return {
      svg: '',
      username: '',
      password: '',
      code: '',
      nickname: '',
      c_password: ''
    }
  },
  mounted () {
    this._getCaptcha()
  },
  components: {},
  methods: {
    _getCaptcha () {
      getCode().then((res) => {
        if (res.code === 200) {
          this.svg = res.data
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.error {
  color: red;
}
.svg {
  position: relative;
  top: -2px;
  cursor: pointer;
}
.error-item{
  position: relative;
  top: -10px;
}
</style>
