<template>
  <q-layout view="hHh Lpr fFf"> <!-- Be sure to play with the Layout demo on docs -->

    <!-- (Optional) The Header -->
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title style="text-align: center">
          Резервация столов
        </q-toolbar-title>
      </q-toolbar>


    </q-header>
    <q-page-container style="display: flex;
  justify-content: center;">
    <q-form
     @submit="onSubmit"
     >
<div class="q-pa-md" >
    <div class="q-gutter-md" style="max-width: 300px">
      <q-input outlined v-model="text" label="Ваше имя" />
         <q-input
        filled
        v-model="phone"
        label="Ваш номер телефона"
        mask="(###) ### - #### - ##"
        fill-mask
        hint="Пример: (380) 000 - 0000 - 00"
      />
        <q-input
      v-model.number="model"
      label="Количество гостей"
      type="number"
      filled
      style="max-width: 300px"
    />
        <div class="q-pa-md" style="max-width: 300px">
    <q-input filled v-model="date">
      <template v-slot:prepend>
        <q-icon name="event" class="cursor-pointer">
          <q-popup-proxy transition-show="scale" transition-hide="scale">
            <q-date v-model="date" mask="YYYY-MM-DD HH:mm">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-date>
          </q-popup-proxy>
        </q-icon>
      </template>
    
      <template v-slot:append>
        <q-icon name="access_time" class="cursor-pointer">
          <q-popup-proxy transition-show="scale" transition-hide="scale">
            <q-time v-model="date" mask="YYYY-MM-DD HH:mm" format24h>
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-time>
          </q-popup-proxy>
        </q-icon>
      </template>
    </q-input>
  </div>
      <q-input outlined v-model="text1" label="Ваши пожелания" />
      <q-btn color="white" text-color="black" type="submit" label="Забронировать стол" />

    </div>
  </div>
  </q-form>

    </q-page-container>

  </q-layout>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'
import  axios  from 'axios'

export default {
  // name: 'LayoutName',

  setup () {
    const $q = useQuasar()
    const text = ref(null)
    const phone = ref(null)
    const model = ref(null)
    const date = ref(null)
    const text1 = ref(null)
    const leftDrawerOpen = ref(false)

    return {  
      date,
      model,
      phone,
      text,
      text1,

      onSubmit () {
        
        
          console.log(text.value)
          console.log(phone.value)
          console.log(model.value)
          console.log(date.value)
          console.log(text1.value)
        var param = {
                    text: text.value,
                    phone: phone.value,
                    model: model.value,
                    date: date.value,
                    text1: text1.value

            };
              let formData = new FormData();
formData.append('text', text.value);
formData.append('phone', phone.value);
formData.append('model', model.value);
formData.append('date', date.value);
formData.append('text1', text1.value);

              
            const str = JSON.stringify(param);
            console.log(str)
            axios({
  method: "post",
  url: "/send.php",
  data: formData
})
  .then(function (response) {
    //handle success
    console.log(response);
  })
  .catch(function (response) {
    //handle error
    console.log(response);
  });
      },

      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
}
</script>
