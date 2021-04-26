<script>
  import { Router, Link, Route } from "svelte-routing";
  import Home from "./Home.svelte";
  import Nav from "./Nav.svelte";
  import Rsvp from "./RSVP.svelte";

  // import About from "./About.svelte";
  // import Blog from "./Blog.svelte";

  export let url = "";
</script>

<Router {url}>
  <Nav />

    <!-- <Route path="blog/:id" component="{BlogPost}" />
    <Route path="blog" component="{Blog}" />
    <Route path="about" component="{About}" /> -->
    <Route path="/"><Home /></Route>
    <Route path="/rsvp"><Rsvp /></Route>
</Router>

<style>
</style>
