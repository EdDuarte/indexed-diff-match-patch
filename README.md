# Indexed DiffMatchPatch in Java

The Diff, Match and Patch Library, originally developed by Neil Fraser and hosted at http://code.google.com/p/google-diff-match-patch/, is a library for detecting in-line text differences (inserted, deleted and unchanged).

This is a fork of that project that changes multiple parts of the algorithm so that **the diffs returned have startIndex and endIndex values**.

The main idea behind this change is to allow a quick retrieval of the difference as-is in the original documents, and the developer can use this value to collect a snippet of the contents surrounding the difference.

All of the required changes to add the string index values where made into a single commit, so if you wish to check the changes and adapt them to other languages that the original project supported, check here: TODO

## Usage ##

### Maven ###
```
<dependency>
    <groupId>com.edduarte</groupId>
    <artifactId>diff-match-patch</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Gradle ###
```
dependencies {
    compile 'com.edduarte:diff-match-patch:1.0.0'
}
```

### Example ###

```java
int snippetOffset = 50, start, end;

// get a snippet of the deleted content (diff
// text plus some surrounding text for context)
start = deletedDiff.startIndex() - snippetOffset;
end = deletedDiff.endIndex() + snippetOffset;
String deletedDiffSnippet = oldText.substring(start, end);

// get a snippet of the inserted content (diff
// text plus some surrounding text for context)
start = insertedDiff.startIndex() - snippetOffset;
end = insertedDiff.endIndex() + snippetOffset;
String insertedDiffSnippet = newText.substring(start, end);
```

This has only been implemented for Java (my primary use-case). You can see this fork in use at https://github.com/vokter/vokter-core.


# License

    Copyright 2015 Eduardo Duarte

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

