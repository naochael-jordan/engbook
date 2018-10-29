<template>
  <section class="container">
    <header>
      <h1>Engbook</h1>
    </header>

    <div class="main">
      <h2>TypeScript</h2>
      <ul>
        <li v-for="(item, index) in list" :key="index">
          <p class="rank">
            <span>{{ index + 1 }}</span>
            位
          </p>
          <p class="word">{{ item.word }}</p>
          <p class="num">
            <span>{{ item.num }}</span>
            回
          </p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";

export default {
  components: {
    AppLogo
  },

  data() {
    return {
      list: []
    };
  },

  created() {
    const results = this.$store.state.ts
      .trim()
      .toLowerCase()
      .replace(/ +/g, " ")
      .replace(/(\r?\n)?(,?\.?)?/g, "")
      .split(" ")
      .reduce((acc, crr) => {
        const index = acc.findIndex(a => a.word === crr);

        if (index === -1) {
          acc.push({
            word: crr,
            num: 1
          });
        } else {
          acc[index].num += 1;
        }

        return acc;
      }, [])
      .sort((a, b) => (a.num > b.num ? -1 : 1));
    this.list = results;
    console.log(results);
  }
};
</script>

<style lang="scss">
.container {
}

header {
  position: relative;
  padding: 12px 0;
  text-align: center;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
}

h2 {
  padding: 4px 0 4px 8px;
  font-size: 16px;
  background-color: #efefef;
}

ul {
  padding: 0;
  list-style: none;
}

li {
  display: flex;
  align-items: center;
  padding: 12px;
  border-bottom: 1px solid #efefef;
}

.rank {
  margin-right: 10px;

  span {
    font-size: 20px;
  }
}

.word {
  flex: 1;
  font-size: 30px;
}

.num {
  span {
    font-size: 20px;
  }
}
</style>

