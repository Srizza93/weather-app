# Weather App

"Weather App" is an application for checking the current weather condition in any city of the world.
It's a Vue component which uses the vue router to show the 2 main pages, the home, which requests an input from the user to select the city, and the weather page that shows the results.
Data is received by the API api.weatherapi.com.
The project was built with Vite via Vue installation with project configuration.
Due to the absence of the server side, web hash history was used for vue router.
This prevents to get a 404 error page from github.

### The routes are

- "/" => Home page, component: HomeView
- "/weather" => Weather page, component: Weather
- "/:pathMatch(._)_" => 404 Page not found

### Demo

[Weather App](https://srizza93.github.io/weather-app/)

### Stack:

- HTML/CSS
- Scss
- Javascript
- Vue
- Vue-router
- Vite
- Api

### Usage

The installation is done via main.js.
The different routes can be found in [/router/index.js](https://github.com/Srizza93/weather-app/blob/main/src/router/index.js).
The routing is handled via single-file component [App.vue](https://github.com/Srizza93/weather-app/blob/main/src/App.vue).

To run the demo:

```
npm install
npm run dev
```

For production:

```
npm run build
```

### Principle

This is the API request

```
   async fetchData() {
      try {
        const url = `https://api.weatherapi.com/v1/current.json?key=9090010261984f75bd8163005222011&q=${this.city}&aqi=no`;
        const response = await fetch(url)
          .then((response) => {
            if (response.ok) {
              return response.json();
            } else if (response.status === 400) {
              this.redirectToNotFound();
              return Promise.reject("Selected city is incorrect");
            } else {
              this.redirectToNotFound();
              return Promise.reject("Something went wrong: " + response.status);
            }
          })
          .then((data) => (this.weather = data));
      } catch (error) {
        console.log("Can't get data from API: " + error);
        this.redirectToNotFound();
      }
    },
```

And this is the input used for the request

```
<div class="input-container">
      <input
        class="input-container_input"
        type="text"
        placeholder="Add your city!"
        v-model="city"
        @keyup.enter="citySelected"
      />
      <div class="input-container_button-wrap">
        <router-link
          class="input-container_button-wrap_button"
          :to="{ name: 'weather', params: { city: city } }"
          >Go!</router-link
        >
      </div>
    </div>
```

- When the user enters the city's name, on enter key up or router-link click, the router will bring the user to the weather page.
- In the weather page the user will see the results from API, which are location info and weather conditions current info.

### Configuration

```
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";

import "./assets/main.css";

const app = createApp(App);

app.use(router);

app.mount("#app");

```

### Style

- Minimalist design developed via single-file components with scoped style, pure CSS and SCSS.
