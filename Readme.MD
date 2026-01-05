npx create-expo-app@latest

Inside the (tabs) you can have different routes , here you will have a \_layout.jsx file

```
import { Tabs } from "expo-router";
import React from "react";

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen
        name="index"
        options={{
          title: "Home",
          headerShown: false,
        }}
      />
      <Tabs.Screen
        name="explore"
        options={{
          title: "Explore",
          headerShown: false,
        }}
      />
    </Tabs>
  );
}


```

The
In the root of the app you can have a \_layout.jsx file

```
import { Stack } from "expo-router";
import { StatusBar } from "expo-status-bar";
import "react-native-reanimated";

export default function RootLayout() {
  return (
    <>
      <Stack>
        <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
        <Stack.Screen name="+not-found" />
      </Stack>
      <StatusBar style="auto" />
    </>
  );
}

```

This will have the Stack Navigator and the Tab Navigator

To create a new route and page , just create a new file in the app (tabs) folder as dashboard.jsx

## Adding Native Wind

npx expo install nativewind tailwindcss@^3.4.17 react-native-reanimated@3.16.2 react-native-safe-area-context

Create a tailwind.config.js file in the root of the project

```
/** @type {import('tailwindcss').Config} */
module.exports = {
  // NOTE: Update this to include the paths to all of your component files.
  content: ["./app/**/*.{js,jsx,ts,tsx}", "./components/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
};

```

Create a global.css file in the root of the project

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

In babel.config.js add the following

```javascript
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ],
  };
};
```

Create a metro.config.js file in the root of the project

```javascript
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require("nativewind/metro");

const config = getDefaultConfig(__dirname);

module.exports = withNativeWind(config, { input: "./global.css" });
```

In your layout , import the global.css file

```javascript
import { Stack } from "expo-router";
import { StatusBar } from "expo-status-bar";
import "react-native-reanimated";
import "../global.css";
export default function RootLayout() {
  return (
    <>
      <Stack>
        <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
        <Stack.Screen name="+not-found" />
      </Stack>
      <StatusBar style="auto" />
    </>
  );
}
```

Incase you get issues with react-native-reanimated , add the following at the top of your entry file (usually App.js or index.js)

```javascript

If that doesn't work, replace useScrollOffset with useScrollViewOffset:
There's been some naming inconsistency in Reanimated. Try this in your component:
javascriptimport Animated, {
  useAnimatedRef,
  useScrollViewOffset,  // Change this
  useAnimatedStyle
} from 'react-native-reanimated';

// Then in your component:
const scrollRef = useAnimatedRef<Animated.ScrollView>();
const scrollOffset = useScrollViewOffset(scrollRef);

```

# Cleaning Up Expo Boilerplate

To delete all the expo boilerplate code , you can delete everything inside the app folder and create a (tabs) folder inside the app folder

```
npm run reset-project
```

# Creating A New Screen

Create a new file called index.jsx inside the (tabs) folder

You can then run "rnfs"

# Setting Up a Welcome Screen

```
import React from "react";
import { SafeAreaView, Text, View } from "react-native";

export default function index() {
  return (
    <SafeAreaView>
      <View className="w-[100%] flex justify-center items-center h-[100vh]">
        <Text className="text-3xl font-bold text-center">Todoist</Text>
        <Text className="text-lg text-center">
          Your everyday app for managing your tasks
        </Text>
      </View>
    </SafeAreaView>
  );
}

```


# Dynamic Routes in Expo Router

- In Your app folder create a new folder called [slug] , this slug parameter can be anything , it is dynamic , think of it as /movies/:id in react-router-dom.



Use the SafeAreaView to avoid the notch on the top of the screen

### Displaying an Image

Have the image in the assets folder

```javascript
<Image
  source={require("../../assets/images/favicon.png")}
  style={{ width: 200, height: 200 }}
/>
```

### Creating A Button

For this we will use TouchableOpacity

```javascript
<TouchableOpacity
  onPress={handlePress}
  className="bg-blue-500 p-4 rounded-lg items-center"
>
  <Text className="text-white font-bold">Press me!</Text>
</TouchableOpacity>
```

#### Handling Presses

We use the onPress function to handle the presses

```javascript
import React from "react";
import {
  Image,
  SafeAreaView,
  Text,
  TouchableOpacity,
  View,
} from "react-native";

export default function index() {
  const actionToDo = () => {
    alert("Hello World");
  };
  return (
    <SafeAreaView>
      <View className="w-[100%] flex justify-center items-center h-[80vh]">
        <Text className="text-3xl font-bold text-center">Todoist</Text>
        <Text className="text-lg text-center">
          Your everyday app for managing your tasks
        </Text>
        <Image
          source={require("../../assets/images/favicon.png")}
          style={{ width: 200, height: 200 }}
        />
        <TouchableOpacity
          onPress={actionToDo}
          className="bg-blue-500 mt-8 p-4 rounded-lg items-center"
        >
          <Text className="text-white font-bold">Press me!</Text>
        </TouchableOpacity>
      </View>
    </SafeAreaView>
  );
}
```

#### Basic Incrimentior

```
import { useState } from "react";
import { SafeAreaView, Text, TouchableOpacity } from "react-native";

export default function calculator() {
  const [result, setResult] = useState(0);

  const incrimemt = () => {
    setResult(result + 1);
  };
  return (
    <SafeAreaView className="bg-gray-100 flex justify-center items-center h-[85vh]">
      <Text className="text-4xl ">Incrimentor</Text>

      <Text className="text-6xl font-semibold">{result}</Text>

      <TouchableOpacity
        className="bg-blue-500  p-3 rounded-md"
        style={{ color: "#fff" }}
        onPress={incrimemt}
      >
        <Text className="text-white">Increment</Text>
      </TouchableOpacity>
    </SafeAreaView>
  );
}

```
