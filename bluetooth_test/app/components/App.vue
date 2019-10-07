<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <GridLayout columns="*" rows="auto,auto,auto">
            <Label class="message" :text="msg" col="0" row="0"/>
            <Label class="message" :text="'enabled:'+ble_enable" col="0" row="1"/>
            <Button text="Button" @tap="bluetooth_check" col="0" row="2"/>
        </GridLayout>

    </Page>
</template>

<script >
  var bluetooth = require("nativescript-bluetooth");

  export default {
    data() {
      return {
        msg: 'Hello World!',
        ble_enable:""
      }
    },
    methods:{
      bluetooth_check : function(){
        let this_ = this;
        bluetooth.isBluetoothEnabled().then(
          function(enabled) {
            console.log("Enabled? " + enabled);
            this_.ble_enable=enabled;
          }
        );
      }
    }
  }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
