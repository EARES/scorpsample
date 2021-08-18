<template>
  <header class="header">
    <b-navbar class="container">
      <template slot="brand">
        <b-navbar-item class="navbar-no--action">
          <b-icon icon="home"> </b-icon>
          <span class="seperator">|</span>
          <span>{{ $route.name }}</span>
        </b-navbar-item>
      </template>
      <template slot="end">
        <b-select v-model="$i18n.locale" class="mt-3">
          <option v-for="(lang, i) in langs" :key="`lang-${i}`" :value="lang">
            {{ lang }}
          </option>
        </b-select>
        <b-navbar-item tag="router-link" :to="{ name: 'Homepage' }">
          Homepage
        </b-navbar-item>
        <b-navbar-item tag="router-link" :to="{ name: 'Contact' }">
          Contact Us
        </b-navbar-item>
        <b-navbar-item tag="div" v-if="username == null">
          <div class="buttons is-flex-mobile is-justify-content-center">
            <b-button type="is-dark" outlined @click="loginmodal = true"
              >Login</b-button
            >
          </div>
        </b-navbar-item>
        <b-navbar-item tag="div" v-if="username != null">
          <div class="buttons">
            <b-dropdown aria-role="list">
              <template #trigger="{ active }">
                <b-button
                  :label="username.name"
                  type="is-primary"
                  :icon-right="active ? 'menu-up' : 'menu-down'"
                />
              </template>

              <b-dropdown-item custom aria-role="menuitem">
                Logged email is <b>{{ useremail.email }}</b>
              </b-dropdown-item>
              <hr class="dropdown-divider" />

              <b-dropdown-item
                value="logout"
                aria-role="menuitem"
                @click="exit"
              >
                <b-icon icon="logout"></b-icon>
                Logout
              </b-dropdown-item>
            </b-dropdown>
          </div>
        </b-navbar-item>
      </template>
    </b-navbar>
    <b-modal
      v-if="username == null"
      v-model="loginmodal"
      has-modal-card
      trap-focus
      aria-role="dialog"
      aria-label="Example Modal"
      aria-modal
    >
      <form>
        <div class="modal-card" style="width: auto">
          <header class="modal-card-head">
            <p class="modal-card-title">Login</p>
            <b-select v-model="$i18n.locale" class="mt-3">
              <option
                v-for="(lang, i) in langs"
                :key="`lang-${i}`"
                :value="lang"
              >
                {{ lang }}
              </option>
            </b-select>
          </header>
          <section class="modal-card-body">
            <b-field label="Title">
              <b-input v-model="form.title" placeholder="Your title"> </b-input>
            </b-field>
            <b-field label="Name">
              <b-input v-model="form.name" placeholder="Your name"> </b-input>
            </b-field>
            <b-field label="Email">
              <b-input
                type="email"
                v-model="form.email"
                placeholder="Your email"
              >
              </b-input>
            </b-field>
            <b-field label="Password">
              <b-input
                type="password"
                v-model="form.pass"
                placeholder="Your password"
              >
              </b-input>
            </b-field>
          </section>
          <footer class="modal-card-foot">
            <b-button expanded label="Close" @click="loginmodal = false" />
            <b-button expanded @click="login" label="Login" type="is-primary" />
          </footer>
        </div>
      </form>
    </b-modal>
  </header>
</template>

<script>
export default {
  data() {
    return {
      langs: ['en', 'tr'],
      username: JSON.parse(localStorage.getItem('userInfo')),
      useremail: JSON.parse(localStorage.getItem('userInfo')),
      loginmodal: false,
      form: {
        title: '',
        name: '',
        email: '',
        pass: '',
      },
    };
  },
  methods: {
    exit() {
      localStorage.clear();
      window.location.reload();
    },
    login() {
      localStorage.setItem('userInfo', JSON.stringify(this.form));
      window.location.reload();
    },
  },
};
</script>

<style scoped>
.navbar {
  min-height: 64px;
}

.header,
.container {
  background-color: #eb6e64;
}

.seperator {
  font-size: 25px;
  margin-left: 10px;
  margin-bottom: -2px;
  margin-right: 8px;
}

.navbar-item {
  color: white;
  font-size: 14px;
}

.navbar-no--action:hover {
  color: white !important;
  cursor: default;
}

.navbar-item:hover,
.navbar-item:focus {
  background-color: #eb6e64;
}
</style>
