Reproduces on clean cache only.
So we run `npm cache clean --force` before each test.
Also cleaning lock file and existing node_modules.

First claim everything works on node 20.18.0:

```
$ asdf local nodejs 20.18.0
$ npm cache clean --force
npm warn using --force Recommended protections disabled.
$ rm -rf node_modules package-lock.json 
$ time npm install --verbose --timing --loglevel silly > 01_node20.18.0+npm.10.8.2.log
... truncated
npm info timing Timing info written to: /home/aleksei_gurianov/.npm/_logs/2024-11-09T13_32_52_629Z-timing.json
npm verbose cwd /home/aleksei_gurianov/ws/test-npm-issue
npm verbose os Linux 6.10.13-3-MANJARO
npm verbose node v20.18.0
npm verbose npm  v10.8.2
npm verbose exit 0
npm info ok
npm install --verbose --timing --loglevel silly >   3,09s user 0,73s system 66% cpu 5,759 total
```

upgrade to npm 10.9.0

```
$ npm i -g npm@10.9.0
$ npm cache clean --force
npm warn using --force Recommended protections disabled.
$ rm -rf node_modules package-lock.json 
$ time npm install --verbose --timing --loglevel silly > 02_node20.18.0+npm.10.9.0.log
... truncated
npm timing idealTree:fixDepFlags Completed in 2ms
npm timing idealTree Completed in 139988ms
npm timing reify:loadTrees Completed in 139989ms
npm timing reify:diffTrees Completed in 4ms
npm silly reify moves {}
npm timing reify:retireShallow Completed in 2ms
npm timing reify:createSparse Completed in 29ms
npm timing reify:loadBundles Completed in 0ms
...truncated
npm timing command:install Completed in 141027ms
npm timing npm Completed in 141351ms
npm info timing Timing info written to: /home/aleksei_gurianov/.npm/_logs/2024-11-09T13_37_57_921Z-timing.json
npm verbose cwd /home/aleksei_gurianov/ws/test-npm-issue
npm verbose os Linux 6.10.13-3-MANJARO
npm verbose node v20.18.0
npm verbose npm  v10.9.0
npm verbose exit 0
npm info ok
npm install --verbose --timing --loglevel silly >   4,23s user 1,10s system 3% cpu 2:21,63 total
```