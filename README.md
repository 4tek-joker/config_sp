# config_supper_app

## usage
```
const resolveURL = Federated.createURLResolver({
    containers: {
      app1: `${Config.APP1_URL?.replace(
        '{platform}',
        Platform.OS,
      )}/[name][ext]`,
      app2: `${Config.APP2_URL?.replace(
        '{platform}',
        Platform.OS,
      )}/[name][ext]`,
    },
  });
```
