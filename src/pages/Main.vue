<template>
  <div>
                  <h3>Регистрация успешная. Ваши данные:</h3>
                  <span>Фамилия: {{ register.surname }}</span><br>
                  <span>Имя: {{ register.firstName }}</span><br>
                  <span>Почта: {{ register.email }}</span><br>

  </div>
</template>

<script>
import {computed, ref, toRefs, watch} from 'vue';
import { mask } from 'vue-the-mask';
import  { useRegisterStore } from '../stores/RegisterStore';
import { useRouter } from 'vue-router';


export default {
    directives: {
        mask
    },
    setup() {
        const register = useRegisterStore();
        return {
            register,
        };
    },

}
</script>

<style scoped>

</style>do