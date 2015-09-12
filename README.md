# ah-stats-plugin
*These methods were removed from the actionHero core for v12, on September 12th, 2015*

This plugin creates methods for you to store arbitrary statistics about your server.  These stats are stored in Redis, and are shared throughout the cluster.

Stats are buffered locally in each induvidual server for a period of time, and then periodically flushed to redis.  You can control these settings via `./config/stats.js`

An example `stats` action is provided which will list back all the stats stored in your cluster, along with metadata about the task system and server. 

## Install

1. `npm install --save ah-stats-plugin`
2. in `./config/plugins.js`, denote the plugin as active:
```
exports['default'] = {
  general: function(api){
    return {
      plugins: [ 'ah-stats-plugin' ]
    };
  }
};
```

## Stats

### api.stats.increment(key, count)
- key is a string of the form ("thing:stuff")
- count is a signed integer (can be negative)

### api.stats.get(key, collection, next)
- next(err, data)
- key is a string of the form ("thing:stuff")
- collection (optional) is one of the collections used for stats set in `api.config.stats.keys`

### api.stats.getAll(collections, next)
- next(err, stats)
- collections (optional) is an array of one or more of the keys used for stats set in `api.config.stats.keys`
- stats is a hash of `{key1: stats {}, key2: stats {} }`
- keys will be collapsed into a hash 