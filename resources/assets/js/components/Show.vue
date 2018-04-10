<template>
    <div class="modal" :class="openmodal">
        <div class="modal-background"></div>
        <div class="modal-card">
          <header class="modal-card-head">
            <p class="modal-card-title">{{ list.name }}'s Details</p>
            <button class="delete" aria-label="close"  @click='close'></button>
          </header>
          <section class="modal-card-body">
            <div class="field">
              <div class="control">
                {{ list.name }}
              </div>
            </div>
            <div class="field">
              <div class="control">
                {{ list.phone }}
              </div>
            </div>
            <div class="field">
              <div class="control">
                {{ list.email }}
              </div>
            </div>
          </section>
          <footer class="modal-card-foot">
            <button class="button" @click='close'>Cancel</button>
          </footer>
        </div>
      </div>
</template>

<script>
  export default {
    props: ['openmodal'],
    data () {
      return {
        list: ""
      }
    },
    methods: {
      close () {
        this.$emit('closeRequest')
      },
      save () {
        axios.post('/phonebook', this.$data.list)
          .then((response) => this.close())
          .catch((error) => this.errors = error.response.data.errors)
      }
    }
  }
</script>