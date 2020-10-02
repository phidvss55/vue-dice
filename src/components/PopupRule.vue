<template>
    <div class="wrapper-rules" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Game Rule</h3>
            <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Obcaecati mollitia doloremque aut necessitatibus voluptate quas? Architecto accusantium ab laudantium, odit neque vero libero, quo ratione veritatis, quidem fuga assumenda. Illo commodi quam itaque ab ullam quibusdam veritatis sint quidem totam, ducimus nulla blanditiis ratione reprehenderit magnam quos velit? Numquam voluptates eius optio id, asperiores ab praesentium perferendis soluta quae maxime laboriosam quaerat minus ipsum harum neque debitis culpa! Iure optio labore, reprehenderit quibusdam minima perspiciatis harum dolor exercitationem deleniti iusto tempore quaerat dolores a unde doloremque qui ea corporis eligendi eaque mollitia molestias illum placeat eius. Unde, quisquam! Natus, laboriosam.</p>
            <button
                v-on:click="confirm"
            >Got It</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'popup-rules',
    props: {
        isOpenPopup: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        confirm: function() {
            this.$emit('confirmEvent')
        }
    },
    computed: {
        getClassPopup: function() {
            return {
                'popup-open': this.isOpenPopup
            }
        }
    }
}
</script>

<style>
.wrapper-rules {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color:  rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
}
.wrapper-rules.popup-open {
    opacity: 1;
    visibility: visible;
}
.rule {
    position: absolute;
    width: 75%;
    margin-left: 13%;
    margin-top: 15%;
    text-align: center;
    background-color: white;
    transition: all 0.3s ease;
}
.rule h3, .rule p, .rule button {   
    padding: 10px 0;
}
.rule button {
    padding: 10px 50px;
    font-size: 15px;
    margin: 10px 0;
}
.rule button:hover {
    background-color: rgb(114, 114, 114);
    border: none;
}
</style>