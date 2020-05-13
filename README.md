# mobile-getting-started
react-native based on `expo`


## Create project
- `expo init myNewProject`
- replace splash and logo images

## Add navigation
- `npm install @react-navigation/native`
- `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`
- add stack nativigation `npm install @react-navigation/stack`
- add to top of entry file `import 'react-native-gesture-handler';`
Usage:
```js
import 'react-native-gesture-handler'
import * as React from 'react';
import { View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

const HomeScreen = ({ navigation }) => {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
       <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
}

const Stack = createStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```
## Add svg support
- ```npm i react-native-svg react-native-svg-transformer```
- add `metro.config.js` file
```js
const { getDefaultConfig } = require("metro-config");
 
module.exports = (async () => {
  const {
    resolver: { sourceExts, assetExts } 
  } = await getDefaultConfig();
  return {
    transformer: {
      babelTransformerPath: require.resolve("react-native-svg-transformer")
    },
    resolver: {
      assetExts: assetExts.filter(ext => ext !== "svg"),
      sourceExts: [...sourceExts, "svg"]
    }
  };
})();
```
- add to `app.json` file
```json
{
  "expo": {
    "packagerOpts": {
      "config": "metro.config.js",
      "sourceExts": ["js", "jsx", "ts", "tsx", "svg"]
    }
  }
}
```
- create `declarations.d.ts` file
```ts
declare module "*.svg" {
  import { SvgProps } from "react-native-svg";
  const content: React.StatelessComponent<SvgProps>;
  export default content;
}
```

Usage:
```js
import Logo from "./logo.svg";

<Logo width={120} height={40} />

```
