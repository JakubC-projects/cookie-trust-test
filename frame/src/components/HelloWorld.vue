<script setup lang="ts">
import {createAuth0Client} from '@auth0/auth0-spa-js'

async function login() {
  const authClient = await createAuth0Client({
    domain: "bcc-sso-sandbox.eu.auth0.com",
    clientId: "2AinYMgKYdFhx8Yg2yn228PpS7JlYOR1",
    authorizationParams: {
      scope: "openid email",
    }
  })
  await authClient.loginWithPopup()
  const token = await authClient.getIdTokenClaims()

  console.log(token)
}
</script>

<template>
    <button type="button" @click="login">login</button>
</template>

