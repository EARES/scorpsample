<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column">
          <form>
            <b-field label="Title">
              <b-input placeholder="Your title" v-model="title"> </b-input>
            </b-field>
            <b-field label="Name">
              <b-input placeholder="Your name" v-model="name"> </b-input>
            </b-field>
            <b-field label="Email">
              <b-input v-model="email" type="email" placeholder="Your email">
              </b-input>
            </b-field>
            <b-field label="Phone number">
              <b-input
                pattern="^[0-9-+\s()]*$"
                type="tel"
                v-model="phone"
                placeholder="Your phone number"
              >
              </b-input>
            </b-field>
            <b-field label="Country">
              <b-autocomplete
                v-model="mdlcountry"
                placeholder="Your Country"
                open-on-focus
                :data="filteredDataObj"
                field="name"
                @select="(option) => (country = option)"
                clearable
              >
              </b-autocomplete>
            </b-field>
            <b-field label="Text">
              <b-input maxlength="200" v-model="text" type="textarea"></b-input>
            </b-field>
            <b-button @click="send" label="Send" type="is-primary" />
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      title: '',
      name: JSON.parse(localStorage.getItem('userInfo')) ? JSON.parse(localStorage.getItem('userInfo')).name : '',
      email: JSON.parse(localStorage.getItem('userInfo')) ? JSON.parse(localStorage.getItem('userInfo')).email : '',
      phone: '',
      text: '',
      country: null,
      mdlcountry: '',
      countryList: [
        { id: 'TR', name: 'Turkey' },
        { id: 'US', name: 'United States of America' },
        { id: 'GB', name: 'United Kingdom' },
        { id: 'DE', name: 'Germany' },
        { id: 'SE', name: 'Sweden' },
        { id: 'KE', name: 'Kenya' },
        { id: 'BR', name: 'Brazil' },
        { id: 'ZW', name: 'Zimbabwe' },
      ],
    };
  },
  methods: {
    send() {
      let postdata = {
        title: this.title,
        name: this.name,
        email: this.email,
        phonenumber: this.phone,
        country_code: this.country.id,
        text: this.text,
      };
      console.log(postdata);
    },
  },
  computed: {
    filteredDataObj() {
      return this.countryList.filter((option) => {
        return (
          option.name
            .toString()
            .toLowerCase()
            .indexOf(this.mdlcountry.toLowerCase()) >= 0
        );
      });
    },
  },
};
</script>
