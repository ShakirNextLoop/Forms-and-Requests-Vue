<template>
<h3>Rating</h3>
  <ul>
    <li>
      <button :class="{active:modelValue=='poor'}" @click="setActiveRating('poor')" type="button">Poor</button>
    </li>
    <li>
      <button :class="{active:modelValue=='average'}" @click="setActiveRating('average')" type="button">Average</button>
    </li>
    <li>
      <button :class="{active:modelValue=='great'}" @click="setActiveRating('great')" type="button">Great</button>
    </li>
  </ul>
</template>

<script>
export default {
    props:['modelValue'],
    emits:['update:modelValue'],
    methods:{
        setActiveRating(rating){
            this.$emit('update:modelValue',rating)
        }
    }
};
</script>

<style scoped>
ul{
    display: flex;
}

li button{
    padding: 20px;
    border: 1px solid gray;
    background: none;
    margin-right: 30px;
}
li{
    list-style: none;
}
.active{
    border: 2px solid red;
    background: rgb(255, 93, 93);
}

</style>