# Rettelse til jeres next.config.js

:bulb:  Efter første gennemgang af løsninger er der en rettelse til selve projektet.

Rettelsen er til for at fjerne uhensigsmæssig fejl-log i jeres console i vscode.

Så lav følgende ændringer for at fjerne fejlen.

Først omdøber vi `next.config.js` til `next.config.mjs` altså med m for module.

Derefter udskifter i inholdet med følgende.

```javascript
const nextConfig = {  
    reactStrictMode: false,
    experimental: {
      serverComponentsExternalPackages: ["mongoose"],
    },
    webpack: function (config, options) {
      console.log(options.webpack.version); // Should be webpack v5 now
      config.experiments = {
        ...config.experiments,
        layers: true,
        topLevelAwait: true,
      };
      return config;
    },
    images: {
      minimumCacheTTL: 0,
      remotePatterns: [],
    }
  }
  
export default nextConfig
```

Nu vil mongoose ikke smide fejl i consollen og vi har en es6 config fremadrettet.

:muscle: Tak for jeres tålmodighed.