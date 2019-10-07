<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <GridLayout columns="*" rows="*">
            <Label class="message" :text="msg" col="0" row="0"/>
        </GridLayout>
    </Page>
</template>

<script >
  import * as application from 'tns-core-modules/application'
  import Vue from 'vue'
  const Event = new Vue()

  application.on(application.launchEvent, (args) => {
      if (args.android) {
          // For Android applications, args.android is an android.content.Intent class.
          console.log("Launched Android application with the following intent: " + args.android + ".");
          Event.$emit("launchEvent")

      } else if (args.ios !== undefined) {
          // For iOS applications, args.ios is NSDictionary (launchOptions).
          console.log("Launched iOS application with options: " + args.ios);
          Event.$emit("launchEvent")
      }
  });

  //アプリを隠した時に呼ばれるイベント的な(バックグランドアプリの起動とかはここでやると良さげ?)
  application.on(application.suspendEvent, (args) => {
      if (args.android) {
          // For Android applications, args.android is an android activity class.
          console.log("!@# suspendEvent Activity: " + args.android);
      } else if (args.ios) {
          // For iOS applications, args.ios is UIApplication.
          console.log("!@# suspendEvent UIApplication: " + args.ios);
      }
  
  });

  //アプリを表に持ってきた時に呼ばれるイベント的な
  application.on(application.resumeEvent, (args) => {
      if (args.android) {
          // For Android applications, args.android is an android activity class.
          console.log("!@# resumeEvent Activity: " + args.android);
      } else if (args.ios) {
          // For iOS applications, args.ios is UIApplication.
          console.log("!@# resumeEvent UIApplication: " + args.ios);
      }
      console.log('!@# resuming for both platforms');
      
  });

  application.on(application.displayedEvent, (args) => {
      // args is of type ApplicationEventData
      console.log("displayedEvent");
  });

  application.on(application.orientationChangedEvent, (args) => {
      // args is of type OrientationChangedEventData
      console.log(args.newValue); // "portrait", "landscape", "unknown"
  });


  application.on(application.exitEvent, (args) => {
      if (args.android) {
          // For Android applications, args.android is an android activity class.
          console.log("!@# exitEvent Activity: " + args.android);
      } else if (args.ios) {
          // For iOS applications, args.ios is UIApplication.
          console.log("!@# exitEvent UIApplication: " + args.ios);
      }
  });

  application.on(application.lowMemoryEvent, (args) => {
      if (args.android) {
          // For Android applications, args.android is an android activity class.
          console.log("!@# lowMemoryEvent Activity: " + args.android);
      } else if (args.ios) {
          // For iOS applications, args.ios is UIApplication.
          console.log("!@# lowMemoryEvent UIApplication: " + args.ios);
      }
  });

  application.on(application.uncaughtErrorEvent, (args) => {
      console.log("!@# uncaughtErrorEvent Error: " + args.error);
  });




  export default {
    created(){
      console.log("created")
      Event.$on("launchEvent", () => {
        console.log("get launch Event!!!")
      })

    },
    data() {
      return {
        msg: 'Hello World!'
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
