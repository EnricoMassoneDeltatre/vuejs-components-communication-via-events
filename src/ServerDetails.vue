<template>
  <div v-if="server">
    <h3>Server {{ server.id }}</h3>
    <form>
      <div class="form-group">
        <label>Status</label>
        <select 
          class="form-control"
          @change="serverStatusChanged">
          <option
            v-for="status in statuses"
            :key="status"
            :value="status"
            :selected="status === server.status">
            {{ status }}
          </option>
        </select>
      </div>
    </form>
  </div>

  <div v-else>
    <h3>
      No server selected
    </h3>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        statuses: ["Normal", "Degraded", "Critical"]
      };
    },

    methods: {
      serverStatusChanged(event) {
        const newServerStatus = event.target.value;
        const { id: serverId } = this.server;

        this.$emit("serverStatusChanged", {
          serverId,
          status: newServerStatus
        });
      }
    },

    props: {
      server: Object
    }
  }
</script>

<style>
</style>