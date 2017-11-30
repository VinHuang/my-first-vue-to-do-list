<template lang="pug">
section.hero.is-primary.is-fullheight
  // Hero head: will stick at the top
  .hero-head
    header.navbar
      .container.has-text-centered
          h1.title.is-1 ZJ's {{title}}          
  // Hero content: will be in the middle
  .hero-body
    .container.has-text-centered
        .notification(v-for="(item, index) in list" :key="item.id" :class="{done: item.isDone}")
            span.tag.is-dark {{index + 1}}.
            p {{item.name}}
            a.button.is-success(@click="done(index)") done
            a.button.is-link(@click="undo(index)") undo
            a.button.is-danger(@click="remove(index)") remove
            div.clear
        .field.has-addons.has-addons-centered
            .control
                input.input(v-model="newItem" placeholder="plz input item name" @keyup.enter="add")
            .control
                a.button.is-info(@click="add") add item
                a.button.is-warning(@click="removeAllDone") remove all done items                   
</template>

<script>
export default {
  data: function() {
    return {
      title: 'To do list',
      list: [
          {name:"do something", isDone: false},
          {name:"do something another", isDone: false}
      ],
      newItem: null
    }
  },
  methods: {
      add: function() {
          if (!!this.newItem) {
            this.list.push({name:this.newItem, isDone: false});
          }
          this.newItem = '';
      },
      remove: function(index) {
          this.list.splice(index,1);
      },
      done: function(index) {
          this.list[index].isDone = true;
      },
      undo: function(index) {
        this.list[index].isDone = false;
      },
      removeAllDone: function() {
          this.list = this.list.filter(item => item.isDone == false);
      }
  }
}
</script>

<style lang="scss" scoped>
    p {
        color: #000;
        float: left;
    }
    span.is-dark {
        float: left;
        margin-right: 10%;
    }
    .notification {
        width: 50%;
        margin: 1.5rem auto;

        a.button {
            float: right;
            margin-left: 2%;
        }

        a.button.is-link {
            display: none;
        }

        &.done {
            background-color: cadetblue;

            p {
                text-decoration: line-through;
            }

            a.button.is-success {
                display: none;
            }

            a.button.is-link {
                display: block;
            }
        }
    }
    div.clear {
        clear: both;
    }
</style>
