# Deploy Images

To deploy, there's some things to consider to start a repo:

* https://github.com/docker/buildx/issues/206

```
#29 [linux/arm/v7 build_prod 1/1] RUN yarn build
#29 41.48 Browserslist: caniuse-lite is outdated. Please run:
#29 41.48   npx update-browserslist-db@latest
#29 41.48   Why you should do it regularly: https://github.com/browserslist/update-db#readme
#29 ...

#23 [linux/arm64 build_prod 1/1] RUN yarn build
#23 41.34 Creating an optimized production build...
#23 43.42 Browserslist: caniuse-lite is outdated. Please run:
#23 43.42   npx update-browserslist-db@latest
#23 43.42   Why you should do it regularly: https://github.com/browserslist/update-db#readme
#23 ...

#29 [linux/arm/v7 build_prod 1/1] RUN yarn build
#29 222.1 Browserslist: caniuse-lite is outdated. Please run:
#29 222.1   npx update-browserslist-db@latest
#29 222.1   Why you should do it regularly: https://github.com/browserslist/update-db#readme
#29 230.5 Compiled successfully.
#29 230.5 
```
