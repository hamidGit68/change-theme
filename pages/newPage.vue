<template>
<div>
  <button @click="changeTheme($event)">default</button>
  <button @click="changeTheme($event)">kind1</button>
  <button @click="changeTheme($event)">kind2</button>
  <button @click="changeTheme($event)">kind3</button>

  <div>
    <pre>
      <code>
        function myFunction() {
          var x = document.getElementById("btn1").name;
          document.getElementById("demo").innerHTML = x;
        }
        let myVar = 56
        let text = "hamid"
        let result = text.substr(1, 4);
      </code>
    </pre>
  </div>
</div>
</template>

<script>
import hljs from 'highlight.js';
export default {
  name: "newPage",
  data() {
    return {
      themeName: "default"
    }
  },

  watch : {
    themeName: function (newValue) {
      console.log(newValue);
      this.asyncImport();
    }
  },

  methods: {
    changeTheme: function (event) {
      this.themeName = event.target.innerText;
    },

    asyncImport: async function () {
      let themeObj = {
        default: "github",
        kind1: "idea",
        kind2: "tomorrow-night-bright",
        kind3: "default"
      }

      await import('highlight.js/styles/' + themeObj[this.themeName] + '.css');

      hljs.highlightAll();
    }
  },

  updated () {
    this.$nextTick(function () {
      hljs.highlightAll();
    });
  }, // increase to ur needs

  mounted() {
    document.onreadystatechange = () => {
      if (document.readyState == "complete") {
        this.asyncImport().then(() => {
          hljs.configure({
            cssSelector: 'pre'
          });
          hljs.highlightAll();
        })

      }
    }
  }
}
</script>

<style scoped>

</style>
