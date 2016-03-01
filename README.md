# cachepy
Module which implements a per GAE instance data cache, similar to what you can achieve with APC in PHP instances.
Each GAE instance caches the global scope, keeping the state of every variable on the global scope. 
You can go farther and cache other things, creating a caching layer for each GAE instance, and it's really fast because
there is no network transfer like in memcache. Moreover GAE doesn't charge for using it and it can save you many memcache
and db requests. 
Not everything are upsides. You can not use it on every case because: 
- There's no way to know if you have set or deleted a key in all the GAE instances that your app is using. Everything you do
  with Cachepy happens in the instance of the current request and you have N instances, be aware of that.
- The only way to be sure you have flushed all the GAE instances caches is doing a code upload, no code change required. 
- The memory available depends on each GAE instance and your app. I've been able to set a 60 millions characters string which
  is like 57 MB at least. You can cache somethings but not everything. 
