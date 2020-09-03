<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h1>{{ articulo.title }}</h1>
        <small>{{ articulo.userId }} - {{ articulo.nombreAutor }}</small>
        <p>{{ articulo.body }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      articulo: "",
      user: ""
    };
  },
  async asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error
  }) {
    try {
      const res = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${params.id}`
      );

      const articulo = res.data;

      const resUser = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${res.data.userId}`
      );

      articulo.nombreAutor = resUser.data.name;

      return { articulo };
    } catch (error) {
      return { error: ReferenceError };
    }
  }
};
</script>
