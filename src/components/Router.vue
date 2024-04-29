<script setup>

</script>

<template>
  <header>
     <div class="wrapper">
       <nav class="navbar navbar-expand-lg bg-body-tertiary">
       </nav>
        <nav class="navbar navbar-expand-lg bg-body-tertiary">
          <div style="background-color: #97c5f0;" class="container-fluid">
            <a class="navbar-brand" href="/"><img width="100" src="/images/flashingLogo.png"></img></a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
              <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
              <div class="navbar-nav">
                <RouterLink class="nav-link" to="/">Home</RouterLink>
                <RouterLink class="nav-link" to="/wedstrijdschema">Wedstrijdschema</RouterLink>
                <RouterLink class="nav-link" to="/admin">Admin</RouterLink>
              </div>  
            </div>
          </div>
        </nav>
     </div>
  </header>
  <RouterView />

 </template>
 
  