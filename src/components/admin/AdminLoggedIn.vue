<script setup>
import SpelerList from '@/components/speler/SpelerList.vue';
import WedstrijdSchemaList from '@/components/wedstrijdschema/WedstrijdSchemaList.vue';
</script>

<template>
<div class="container-fluid">
<h2>Admin</h2>
 <div class="row">
    <div class="col-2">
      <div id="list-example" class="list-group">
        <a class="list-group-item list-group-item-action" href="#list-item-1">Accounts</a>
        <a class="list-group-item list-group-item-action" href="#list-item-2">WedstrijdSchema</a>
      </div>
    </div>
    <div class="col-8">
      <div data-bs-spy="scroll" data-bs-target="#list-example" data-bs-smooth-scroll="true" class="scrollspy-example" tabindex="0">
        <div id="list-item-1" class="container">
            <SpelerList></SpelerList>
        </div>
        <div id="list-item-2" class="container">
            <WedstrijdSchemaList></WedstrijdSchemaList>
        </div>
      </div>
    </div>
 </div>
</div>

</template>
