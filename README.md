

# react-native-template

 Project folders template and library for ****React Native****

# Folders structure
**Project Name**
- **src**
	-  ***@types***
		-  png
		- svg
	 - ***assets***
		 -  png
		 - svg
	 - ***global***
	     - theme
	 - ***routers***
	 - ***components***
	 - ***screens***

# Essentials Library

 - **Name:** Styled-Components <pre>`yarn add styled-Components`</pre>
	 - **Dependency:** @types styled-components-react-native <pre>`yarn add @types/styled-components-react-native -D`</pre>
- **Name:** Responsive-fontsize <pre>`yarn add react-native-responsive-fontsize`</pre>
- **Name:** Iphone-x-helper <pre>`yarn add react-native-iphone-x-helper`</pre>
- **Name:** React-navigation <pre>`yarn add @react-navigation/native`</pre>
	- **Dependency:** 
		- React-native-screens, react-native-safe-area-context <pre>`yarn add react-native-screens react-native-safe-area-context`
		- Bottom-tabs <pre>`yarn add @react-navigation/bottom-tabs`</pre>

# Essentials Image Library:

 - **Name:** React-native-svg <pre>`expo install react-native-svg`</pre>
	 - **Dependency:** Svg-transformer <pre>`yarn add --dev react-native-svg-transformer`</pre>
	 **For Expo SDK v41.0.0 or newer**</br>
	 	For the svg to work, replace your *metro.config.js* with the one below.
		```javascript
		const { getDefaultConfig } = require("expo/metro-config");

		module.exports = (() => {
		  const config = getDefaultConfig(__dirname);

		  const { transformer, resolver } = config;

		  config.transformer = {
		    ...transformer,
		    babelTransformerPath: require.resolve("react-native-svg-transformer"),
		  };
		  config.resolver = {
		    ...resolver,
		    assetExts: resolver.assetExts.filter((ext) => ext !== "svg"),
		    sourceExts: [...resolver.sourceExts, "svg"],
		  };

		  return config;
		})();
		```
		
# Custom fonts:
- **Name:** *open-sans*(change this name in the command to match your font) <pre>`expo install expo-font @expo-google-fonts/open-sans`</pre>
	- **Install the expo-splash-screen**
			<pre>`expo install expo-splash-screen`</pre>

	- **In *App.js/.tsx*, import the SplashScreen**
	    ```javascript 
	    import * as SplashScreen from 'expo-splash-screen';
	    ```
	- **In *App.js/.tsx* add preventAutoHideAsync up export default App()**
	```javascript 
	// Keep the splash screen visible while we search for resources
	SplashScreen.preventAutoHideAsync(); // add it up export default function App() {}
	```
	- **In *App.js/.tsx* add this code bellow export default function**
	```javascript
	const [fontsLoaded] = useFonts({
	    OpenSans_400Regular,
	    OpenSans_600SemiBold
	});

	const onLayoutRootView = useCallback(async () => {
	    if (fontsLoaded) {
		await new Promise(resolve => setTimeout(resolve, 2000)); // Delete it or add your time to load.

		await SplashScreen.hideAsync();
	    }
	}, [fontsLoaded]);

	if (!fontsLoaded) {
	    return null;
	}
	```

	**App.tsx/.js, in return add onLayoutRootView**
	```javascript 
	return (
	    onLayoutRootView(), // add this
	    <ThemeProvider theme={theme}>
		<Home />
	    </ThemeProvider>
	)
	```
