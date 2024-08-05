<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtWelcome />
  </div>
</template>

<script setup>
  const { data: user, execute: executeFetchUser } = useFetch('https://reqres.in/api/users/23', {
    immediate: false,
  });

  async function fetchUser() {
    await executeFetchUser();

    console.log('do some extra stuff after fetching user');
  }

  await fetchUser();

  /** Wrong use of useFetch but DOES deduplicate request it seems */
  async function fetchUser2() {
    const { data: user } = await useFetch('https://reqres.in/api/users/23');

    console.log('do some extra stuff after fetching user');
  }

  await fetchUser2();
</script>
