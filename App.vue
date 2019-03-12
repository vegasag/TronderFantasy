<template>
  <app-navigation></app-navigation>
</template>

<script>
import { StackNavigator } from "vue-native-router";
import MainScreen from "./Main";
// import Header from './src/components/Header';
import ThomasScreen from "./src/screens/Thomas";

const AppNavigation = StackNavigator(
  {
    Main: MainScreen,
    Thomas: ThomasScreen,
  },
  {
    initialRouteName: 'Main',
  }
);
export default {
    components: { AppNavigation }
}
</script>