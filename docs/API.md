# API and Configuration

## Available imports
- `Router`
- `Scene`
- `Tabs`
- `Tabbed Scene`
- `Drawer`
- `Modal`
- `Lightbox`
- `Actions`
- `ActionConst`

## Router:

| Property | Type | Default | Description |
|-------------|----------|--------------|----------------------------------------------------------------|
| children |  | required | Scene root element |
| `wrapBy`   | `Function` |  | allows integration of state management schemes like Redux (`connect`) and Mobx (`observer`) |
| `sceneStyle`     | `Style` |  | Style applied to all scenes (optional) |

## Scene:
The basic routing component for this router, all `<Scene>` components require a `key` prop that must be unique. A parent `<Scene>` cannot not have a `component` as a `prop` as it will act as a grouping component for its children.

| Property | Type | Default | Description |
|-----------|----------|----------|--------------------------------------------|
| `key`       | `string` | `required` | Will be used to call screen transition, for example, `Actions.name(params)`. Must be unique. |
| `component` | `React.Component` | `semi-required` | The `Component` to be displayed. Not required when defining a nested `Scene`, see example. |
| `animationEnabled`     | `boolean` | `true` | Enable or disable animating tabs on switch. |
| `back`     | `boolean` | `false` | If it is `true` back button is displayed instead of left/drawer button defined by upper container. |
| `init`     | `boolean` | `false` | If it is `true` back button will not be displayed |
| `clone`     | `boolean` | `false` | Scenes marked with `clone` will be treated as templates and cloned into the current scene's parent when pushed. See example. |
| `contentComponent`     | `React.Component` |  | Component used to render the content of the drawer (e.g. navigation items). |
| `drawer`     | `boolean` | `false` | load child scenes inside [DrawerNavigator](https://reactnavigation.org/docs/navigators/drawer) |
| `failure` | `Function` | | If `on` returns a "falsey" value then `failure` is called. |
| `headerBackTitle` | `string` |  | Specifies the back button title for scene |
| `headerMode` | `string` | `float` | Specifies how the header should be rendered: `float` (render a single header that stays at the top and animates as screens are changed. This is a common pattern on iOS.), `screen` (each screen has a header attached to it and the header fades in and out together with the screen. This is a common pattern on Android) or `none` (No header will be rendered) |
| `hideNavBar`     | `boolean` | `false` | hide the nav bar |
| `hideTabBar`     | `boolean` | `false` | hide the tab bar (only applies to scenes with `tabs` specified) |
| `initial`   | `boolean` | `false` | Set to `true` if this is the first scene to display among its sibling `Scene`s |
| `leftButtonImage`     | `Image` |  | Image to substitute for the left nav bar button |
| `leftButtonTextStyle`     | `Style` |  | Style applied to left button text |
| `modal`     | `boolean` | `false` |  Defines scene container as 'modal' one, i.e. all children scenes will have bottom-to-top animation. It is applicable only for containers (different from v3 syntax) |
| `navBar` | `React.Component`| | Optional React component to render custom NavBar |
| `navBarButtonColor` | `string` | | Set the color of the back button in the navBar |
| `navigationBarStyle`     | `Style` | | Style applied to nav bar |
| `navigationBarTitleImage` | `Image` | | Override the image in the center of the navbar, replacing the `title` |
| `navigationBarTitleImageStyle` | `object` | | Styles to apply to `navigationBarTitleImage` |
| `navTransparent`     | `boolean` | `false` | nav bar background transparency |
| `on`     | `Function` | | aka `onEnter` |
| `onEnter`     | `Function` | | Called when the `Scene` is navigated to. `props` are provided as a function param. Only scenes with 'component' defined is supported |
| `onExit`     | `Function` | | Called when the `Scene` is navigated away from. Only scenes with 'component' defined is supported |
| `onLeft`     | `Function` |  | Called when the left nav bar button is pressed. |
| `onRight`     | `Function` |  | Called when the right nav bar button is pressed. |
| `renderTitle`     | `React.Component` |  | React component to render title for nav bar |
| `rightButtonImage`     | `Image` |  | Image to substitute for the right nav bar button |
| `rightButtonTextStyle`     | `Style` |  | Style applied to right button text |
| `success`     | `Function` | | If `on` returns a "truthy" value then `success` is called. |
| `tabs`     | `boolean` | `false` | load child scenes as [TabNavigator](https://reactnavigation.org/docs/navigators/tab). Other [Tab Navigator  props](https://reactnavigation.org/docs/navigators/tab#TabNavigatorConfig) also apply here. |
| `title`     | `string` |  | Text to be displayed in the center of the nav bar. |
| `titleStyle`     | `Style` |  | Style applied to the title |
| `type`   | `string` | `push` | Optional type of navigation action. You could use `replace` to replace current scene with this scene |
| all other props     |  |  | Any other props not listed here will be pass on to the specified `Scene`'s `component` |

## Tabs (`<Tabs>` or `<Scene tabs>`)
Can use all `props` listed above in `<Scene>` as `<Tabs>` is syntatic sugar for `<Scene tabs={true}>`.

| Property | Type | Default | Description |
|-----------------|----------|----------|--------------------------------------------|
| `wrap`     | `boolean` | `true` | Wrap each scene with own navbar automatically (if it is not another container). |
| `activeBackgroundColor` | `string` |  | Specifies the active background color for the tab in focus |
| `activeTintColor`     | `string` |  | Specifies the active tint color for tabbar icons |
| `inactiveBackgroundColor` | `string` |  | Specifies the inactive background color for the tabs not in focus |
| `inactiveTintColor`     | `string` |  | Specifies the inactive tint color for tabbar icons |
| `labelStyle` | `object` | | Overrides the styles for the tab label |
| `lazy`     | `boolean` | `false` | Won't render/mount the tab scene until the tab is active |
| `tabBarComponent`     | `React.Component` |  | React component to render custom tab bar |
| `tabBarPosition`     | `string` |  | Specifies tabbar position. Defaults to `bottom` on iOS and `top` on Android. |
| `tabBarStyle` | `object` | | Override the tabbar styles |
| `tabStyle` | `object` | | Override the style for an individual tab of the tabbar |
| `showLabel`     | `boolean` | `true`  | Boolean to show or not the tabbar icons labels |
| `swipeEnabled`     | `boolean` | `true` | Enable or disable swiping tabs. |

## Stack (`<Stack>`)
A component to group Scenes together for its own stack based navigation. Using this will create a separate havigator for this stack, so expect two navbars to appear unless you add `hideNavBar`.

## Tab Scene (child `<Scene>` within `Tabs`)
A `Scene` that is a direct child of `Tabs` and can use all `props` listed above in `Scene`,

| Property | Type | Default | Description |
|-----------------|----------|----------|--------------------------------------------|
| `icon` | `component` | `undefined` | a React Native component to place as a tab icon
| `tabBarLabel` | `string` | | The string to override a tab label |

## Drawer (`<Drawer>` or `<Scene drawer>`)
Can use all `prop` as listed in `Scene` as `<Drawer>`, syntatic sugar for `<Scene drawer={true}>`

| Property | Type | Default | Description |
|---|---|---|---|
| `drawerImage` | `Image` |  | Image to substitute drawer 'hamburger' icon, you have to set it together with `drawer` prop |
| `drawerIcon` | `React.Component` |  | Arbitrary component to be used for drawer 'hamburger' icon, you have to set it together with `drawer` prop |
| `drawerPosition` | `string`  | Determines whether the drawer is on the right or the left. Keywords accepted are `right` and `left` |


## Modals (`<Modal>` or `<Scene modal>`)
To implement a modal, you must use `<Modal>` as the root scene in your `Router`. The `Modal` will render the first scene (should be your true root scene) normally, and all following
To display a modal use `<Modal>` as root renderer, so it will render the first element as `normal` scene and all others as popups (when they are pushed).

Example:
In the example below, the `root` Scene is nested within a `<Modal>`, since it is the first nested `Scene`, it will render normally. If one were to `push` to `statusModal`, `errorModal` or `loginModal`, they will render as a `Modal` and by default will pull up from the bottom of the screen. It is important to note that currently the `Modal` does not allow for transparent backgrounds.

```jsx
//... import components
<Router>
  <Modal>
    <Scene key="root">
      <Scene key="screen1" initial={true} component={Screen1} />
      <Scene key="screen2" component={Screen2} />
    </Scene>
    <Scene key="statusModal" component={StatusModal} />
    <Scene key="errorModal" component={ErrorModal} />
    <Scene key="loginModal" component={LoginModal} />
  </Modal>
</Router>
```

## Lightbox (`<Lightbox>`)
Lightbox is a component used to render a component on top of the current `Scene`. Unlike modal, it will allow for resizing and transparency of the background.

Example:
In the example below, the `root` Scene is nested within a `<Lightbox>`, since it is the first nested `Scene`, it will render normally. If one were to `push` to `loginLightbox`, they will render as a `Lightbox` and by default will lay on top of the current `Scene` allowing for transparent backrounds.

```jsx
//... import components
<Router>
  <Lightbox>
    <Scene key="root">
      <Scene key="screen1" initial={true} component={Screen1} />
      <Scene key="screen2" component={Screen2} />
    </Scene>

    {/* Lightbox components will lay over the screen, allowing transparency*/}
    <Scene key="loginLightbox" component={loginLightbox} />
  </Lightbox>
</Router>
```

## Actions
This `Object` is the main utility is to provide navigation features to your application. Assuming your `Router` and `Scenes` are configured properly, use the properties listed below to navigate between scenes. Some offer the added functionality to pass React `props` to the navigated scene.

These can be used directly, for example, `Actions.pop()` will dispatch correspond action written in the source code, or, you can set those constants in scene type, when you do Actions.main(), it will dispatch action according to your scene type or the default one.

| Property | Type | Parameters | Description |
|-----------------|----------|----------|--------------------------------------------|
| `[key]` | `Function` | `Object` | The `Actions` object "automagically" uses the `Scene`'s `key` prop in the `Router` to navigate. To navigate to a scene, call `Actions.key()` or `Actions[key].call()`. |
| `jump` | `Function` | `(sceneKey: String, props: Object)` | used to switch to a new tab. For `Tabs` only. |
| `pop` | `Function` | | Go back to the previous scene by "popping" the current scene off the nav stack |
| `popAndPush` | `Function` | `(sceneKey: String, props: Object)` |
| `popTo` | `Function` | `(sceneKey: String, props: Object)` | Pops the stack until the
| `push` | `Function` | `(sceneKey: String, props: Object)` | Pushes the scene to the stack, performing a transition to the new scene. |
| `refresh` | `Function` | `(props: Object)` | Reloads the current scene by loading new `props` into the `Scene` |
| `replace` | `Function` | `(sceneKey: String, props: Object)` |  Pops the current scene from the stack and pushes the new scene to the navigation stack. *No transition will occur. |
| `reset` | `Function` | `(sceneKey: String, props: Object)` | Clears the routing stack and pushes the scene into the first index. *No transition will occur.* |
| `drawerOpen` | `Function` | | Opens the `Drawer` if applicable |
| `drawerClose` | `Function` | | Closes the `Drawer` if applicable |

## ActionConst
Type constants to determine `Scene` transitions, These are **PREFERRED** over typing their values manually as these are subject to change as the project is updated.

| Property | Type | Value | Shorthand |
|-----------------|----------|----------|--------------------------------------------|
| `ActionConst.JUMP` | `string` | 'REACT_NATIVE_ROUTER_FLUX_JUMP' | `jump` |
| `ActionConst.PUSH` | `string` | 'REACT_NATIVE_ROUTER_FLUX_PUSH' | `push` |
| `ActionConst.PUSH_OR_POP` | `string` | 'REACT_NATIVE_ROUTER_FLUX_PUSH_OR_POP' | `push` |
| `ActionConst.REPLACE` | `string` | 'REACT_NATIVE_ROUTER_FLUX_REPLACE' | `replace` |
| `ActionConst.BACK` | `string` | 'REACT_NATIVE_ROUTER_FLUX_BACK' | `pop` |
| `ActionConst.BACK_ACTION` | `string` | 'REACT_NATIVE_ROUTER_FLUX_BACK_ACTION' | `pop` |
| `ActionConst.POP_TO` | `string` | 'REACT_NATIVE_ROUTER_FLUX_POP_TO' | `popTo` |
| `ActionConst.REFRESH` | `string` | 'REACT_NATIVE_ROUTER_FLUX_REFRESH' | `refresh` |
| `ActionConst.RESET` | `string` | 'REACT_NATIVE_ROUTER_FLUX_RESET' | `reset` |
| `ActionConst.FOCUS` | `string` | 'REACT_NATIVE_ROUTER_FLUX_FOCUS' | *N/A* |
| `ActionConst.BLUR` | `string` | 'REACT_NATIVE_ROUTER_FLUX_BLUR' | *N/A* |
| `ActionConst.ANDROID_BACK` | `string` | 'REACT_NATIVE_ROUTER_FLUX_ANDROID_BACK' | *N/A* |
