<script>
  import createRouter, { ROUTER_MODE, router } from '@spaceavocado/svelte-router';
  import RouterView from '@spaceavocado/svelte-router/component/view';
  import Home from '../views/Home.svelte';

  // Webpack dynamic import
  const asyncView = (view) => {
    return new Promise((resolve) => {
      const component = import(/* webpackChunkName: "view-[request]" */ `../views/${view}.svelte`);
      resolve(component);
    });
  };

  createRouter({
    mode: ROUTER_MODE.HISTORY,
    routes: [
      {
        path: '/',
        name: 'HOME',
        component: Home,
      },
      {
        path: '/teste',
        name: 'TESTE',
        component: asyncView(`Teste`),
        props: true,
      },
    ],
  });
</script>

<RouterView />
