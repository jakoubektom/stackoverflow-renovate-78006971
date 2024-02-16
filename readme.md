
[Stack overflow question](https://stackoverflow.com/questions/78006971/renovate-prevent-query-for-local-dependencies-in-maven)

----------------------------

I have maven multi module project.

Parent pom.xml:
```xml
<groupId>com.group</groupId>
<artifactId>product-parent</artifactId>
<version>1.0.0-SNAPSHOT</version>
```

Child pom.xml:
```xml
<parent>
    <groupId>com.group</groupId>
    <artifactId>product-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <relativePath>../pom.xml</relativePath>
</parent>
<artifactId>product</artifactId>
```

When I run Renovate I see in log that `product-parent` dependency is queried to maven central. But I want Renovate to ignore local (in project) dependencies - in other words, **ignore dependencies when dependency have filled in `relativePath`**.

This behavior has other side effects such as when release version of local dependency exists, Renovate prioritize it over `SNAPSHOT` (unstable) and creates merge/pull request on this `product-parent` dependency which is for local dependencies unwanted behavior.


Tested with self hosted renovate v37.173

As workaround I list all affected local parent poms in `ignoreDeps`