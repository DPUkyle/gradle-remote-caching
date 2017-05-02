# gradle-remote-caching

Simple project to demonstrate cache misses when using a remote cache server.

## Prerequisites
Two different build machines, ideally with drastically different operating systems and default encodings.

In my case, I have a linux OS (UTF-8, naturally) and a Japanese Windows OS (MS932 a.k.a Shift-JIS).
 
## Steps to run
 1. Clone this repo in both environments
 2. Modify the `buildCacheUrl` value in gradle.properties to match your own remote cache backend.
 3. On the _first_ build machine:
    1. $ git clean -dfxq
    2. $ ./gradlew build
    3. assert results like: 
    ```
    22 tasks in build, out of which 10 (45%) were executed
     4  (18%) up-to-date
     8  (36%) no-source
     2   (9%) cache miss
     8  (36%) not cacheable
    ```
 4. On the _second_ build machine:
    1. git clean -dfxq
    2. gradlew build
    3. assert results like: 
    ```
    22 tasks in build, out of which 6 (27%) were executed
     6  (27%) up-to-date
     8  (36%) no-source
     2   (9%) loaded from cache
     6  (27%) not cacheable
    ```