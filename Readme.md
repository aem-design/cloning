## Summary

[![build_status](https://github.com/aem-design/cloning/workflows/build/badge.svg?branch=master)](https://github.com/aem-design/cloning/actions?workflow=build)
[![release_status](https://github.com/aem-design/cloning/workflows/release-to-maven-central/badge.svg?branch=master)](https://github.com/aem-design/cloning/actions?workflow=release-to-maven-central)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/design.aem/cloning/badge.svg?magic)](https://maven-badges.herokuapp.com/maven-central/design.aem/cloning)
[![github license](https://img.shields.io/github/license/aem-design/cloning)](https://github.com/aem-design/cloning)
[![github issues](https://img.shields.io/github/issues/aem-design/cloning)](https://github.com/aem-design/cloning)
[![github last commit](https://img.shields.io/github/last-commit/aem-design/cloning)](https://github.com/aem-design/cloning)
[![github repo size](https://img.shields.io/github/repo-size/aem-design/cloning)](https://github.com/aem-design/cloning)
[![github repo size](https://img.shields.io/github/languages/code-size/aem-design/cloning)](https://github.com/aem-design/cloning)
[![github release](https://img.shields.io/github/release/aem-design/cloning)](https://github.com/aem-design/cloning)
[![Visit AEM.Design](https://img.shields.io/badge/visit-aem.design-brightgreen)](https://aem.design/)

The cloning library is a small, open source (Apache licensed) Java library which deep-clones objects. The objects don't have to implement the Cloneable interface. Effectively, this library can clone ANY Java object. It can be used i.e. in cache implementations if you don't want the cached object to be modified or whenever you want to create a deep copy of objects.

Here is an example of its usage:

```java
Cloner cloner = new Cloner();

MyClass clone = cloner.deepClone(o);
// clone is a deep-clone of o
```

**IMPORTANT** : deep cloning of Java classes might mean thousands of objects are cloned! Also cloning of files and streams might make the JVM crash. Enable dumping of cloned classes to stdout during development is highly recommended in order to view what is cloned.

## Useful links
  * [Usage details and examples](USAGE.md)
  * [Development](DEVELOPMENT.md)
 
 
## Using

### Maven

you can add this as a dep

```xml
    <dependencies>
        <dependency>
            <groupId>design.aem</groupId>
            <artifactId>cloning</artifactId>
            <version>1.11.0</version>
        </dependency>
    </dependencies>
```
 
## What is this for

### ObjectInputStream

You can try simple ObjectInputStream copy:

```
ObjectType copy = null;
try {
    // Write the object out to a byte array
    ByteArrayOutputStream bos = new ByteArrayOutputStream();
    ObjectOutputStream out = new ObjectOutputStream(bos);
    out.writeObject(this);
    out.flush();
    out.close();

    // Read input stream into a copy of the object.
    ObjectInputStream in = new ObjectInputStream(new ByteArrayInputStream(bos.toByteArray()));
    copy = (ObjectType) in.readObject();
} catch (IOException e) {
    e.printStackTrace();
} catch (ClassNotFoundException cnfe) {
    cnfe.printStackTrace();
}
return copy;
```

### Alternative

Another approach that could work is using gson:

```
    Gson gson = new GsonBuilder().create();
    String json = gson.toJson(this);
    copy = gson.fromJson(json, FormDataModel.class);
```

