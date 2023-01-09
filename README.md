# config_supper_app

# Note config build mini app

## Add asset and svg config in mini app

```
module: {
    rules: [
      .....
      {
        test: Repack.getAssetExtensionsRegExp(
          Repack.ASSET_EXTENSIONS.filter(ext => ext !== 'svg'),
        ),
        use: {
          loader: '@callstack/repack/assets-loader',
          options: {
            platform,
            inline: true, // add new for use image in line
            devServerEnabled: Boolean(devServer),
            /**
              * Defines which assets are scalable - which assets can have
              * scale suffixes: `@1x`, `@2x` and so on.
              * By default all images are scalable.
              */
            scalableAssetExtensions: Repack.SCALABLE_ASSETS,
          },
        },
      },
      {
        test: /\.svg$/,
        use: [
          {
            loader: '@svgr/webpack',
            options: {
              native: true,
              dimensions: false,
            },
          },
        ],
      },
  ....
  plugins: [
```
## Add lib native
```
rules: [
    {
      test: /\.[jt]sx?$/,
      include: [
        /node_modules(.*[/\\])+react/,
        /node_modules(.*[/\\])+@react-native/,
        /node_modules(.*[/\\])+@react-navigation/,
        /node_modules(.*[/\\])+@react-native-community/,
        /node_modules(.*[/\\])+@expo/,
        /node_modules(.*[/\\])+pretty-format/,
        /node_modules(.*[/\\])+metro/,
        /node_modules(.*[/\\])+abort-controller/,
        /node_modules(.*[/\\])+@callstack\/repack/,
        
        /**
        * add lid module 
        * example /node_modules(.*[/\\])+react-native-video/ 
        * add in supper app (lib native and lib js)
        */
      ],
      use: 'babel-loader',
    },
    ...
```

```
new Repack.plugins.ModuleFederationPlugin({
    ....
      'react-native-video': {
        ...Repack.Federated.SHARED_REACT_NATIVE,
        eager: true,    /// only add miniapp
        requiredVersion: '^5.2.1',
      },
    },
  }),
```
## Add lib js
```
'react-native-fast-image': {
      ...Repack.Federated.SHARED_REACT,
      eager: true,    /// only add miniapp
      requiredVersion: '^8.6.1',
    },
```