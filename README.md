# Indexed DiffMatchPatch in Java

[![Build Status](https://travis-ci.org/edduarte/indexed-diff-match-patch.svg?branch=master)](https://travis-ci.org/edduarte/indexed-diff-match-patch)

The Diff, Match and Patch Library, originally developed by Neil Fraser and hosted at http://code.google.com/p/google-diff-match-patch/, is a library for detecting in-line text differences ('inserted' and 'deleted').

This is a fork of the DiffMatchPatch project that changes multiple parts of the algorithm so that **diffs returned have a startIndex and an endIndex value**.

The main idea behind this fork comes from the fact that character-based index pointers are required for a great majority of NLP tools available (e.g.: sentence-splitters, roi taggers). Using ```String.indexOf(diffText)``` or ```String.lastIndexOf(diffText)``` to obtain these indexes would not be a viable solution, since a diff text can often occur multiple times in the same document.

Other use cases include sorting diffs by startIndex (so that they are ordered by occurrence in the original document) and using ```String.substring()``` to retrieve text surrounding the differed section (snippets).

## Usage

### Maven
```
<dependency>
    <groupId>com.edduarte</groupId>
    <artifactId>diff-match-patch</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Gradle
```
dependencies {
    compile 'com.edduarte:diff-match-patch:1.0.0'
}
```

## Example

```java
DiffMatchPatch dmp = new DiffMatchPatch();
LinkedList<Diff> diffs = dmp.diff_main(oldText, newText);

int snippetOffset = 50;
for (Diff d : diffs) {

    int start = d.getStartIndex() - snippetOffset;
    int end = d.getEndIndex() + snippetOffset;

    if (d.getOperation().equals(DiffMatchPatch.Operation.INSERT)) {

        // for diffs with operation 'INSERT', the snippet is a
        // substring of the newText
        String snippet = newText.substring(start, end);

    } else if (d.getOperation().equals(DiffMatchPatch.Operation.DELETE) ||
               d.getOperation().equals(DiffMatchPatch.Operation.EQUAL)) {

        // for diffs with operation 'DELETE' or 'EQUAL', the snippet is a
        // substring of the oldText
        String snippet = oldText.substring(start, end);

    }
}
```


## Projects using this library

You can see this library in use at https://github.com/vokter/vokter.


# License

    Copyright 2016 Eduardo Duarte

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

