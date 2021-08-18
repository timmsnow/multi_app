<template>
  <div>
    <label class="typo__label">Simple select / dropdown</label>
    <multiselect
      v-model="value"
      :options="options"
      :multiple="true"
      :close-on-select="false"
      :clear-on-select="false"
      :preserve-search="true"
      placeholder="Pick some"
      label="name"
      track-by="name"
      :preselect-first="true"
    >
      <template slot="selection" slot-scope="{ values, search, isOpen }">
        <span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">
          {{ values.length }} options selected
        </span>
      </template>
    </multiselect>
    <!-- <pre class="language-json"><code>{{ value  }}</code></pre> -->
    <!-- {{ value }} -->
    <button v-on:click="postIt()">BUTTONS</button>
  </div>
</template>

<script>
import Multiselect from "vue-multiselect";
import axios from "axios";

export default {
  components: {
    Multiselect,
  },
  data() {
    return {
      value: [],
      options: [],
    };
  },
  created: function () {
    this.getJobs();
  },
  methods: {
    getJobs: function () {
      axios.get("http://localhost:3000/api/users").then((response) => {
        response.data.forEach((item) => {
          console.log(item);
          var object = {};
          object["name"] = item.name;
          object["id"] = item.id;
          this.options.push(object);
        });
        console.log(this.options);
      });
    },
    postIt: function () {
      console.log(this.value);
    },
  },
};
</script>
