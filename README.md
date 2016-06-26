# Indexed DiffMatchPatch in Java

The Diff, Match and Patch Library, originally developed by Neil Fraser and hosted at http://code.google.com/p/google-diff-match-patch/, is a library for detecting in-line text differences ('inserted' and 'deleted').

This is a fork of that project that changes multiple parts of the algorithm so that **the diffs returned have a startIndex and a endIndex value**.

The main idea behind this fork is to allow a quick retrieval of diff text as-is in the original documents for further parsing purposes. Sentence-splitting can be used to collect the entire sentence where the diff occurred, and ```String.substring()``` can be used to retrieve text surrounding the differed section (snippets). Note that using ```String.indexOf(diffText)``` or ```String.lastIndexOf(diffText)``` after executing the original algorithm would not be a viable solution, since a diff text can often occur multiple times in the same document.

This has only been implemented for Java (my primary use-case). All of the required changes to add the string index values where made into a single commit, so if you wish to check the changes and adapt them to the other languages supported originally, check here: https://github.com/edduarte/indexed-diff-match-patch/commit/45132be9ac6246a7cb8f574fd26f90bf02d1b294

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
DiffMatchPatch dmp = new DiffMatchPatch();
LinkedList<Diff> diffs = dmp.diff_main(oldText, newText);

int snippetOffset = 50;
for (Diff d : diffs) {

    int start = d.getStartIndex() - snippetOffset;
    int end = d.getEndIndex() + snippetOffset;

    // for diffs with operation 'DELETE', the snippet is a substring on the oldText
    String deletedDiffSnippet = oldText.substring(start, end);

    // for diffs with operation 'INSERT', the snippet is a substring on the newText
    String insertedDiffSnippet = newText.substring(start, end);

}
```

You can see this fork in use at https://github.com/vokter/vokter-core.


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

