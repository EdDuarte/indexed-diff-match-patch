# Indexed DiffMatchPatch in Java

The Diff, Match and Patch Library, originally developed by Neil Fraser and hosted at http://code.google.com/p/google-diff-match-patch/, is a library for detecting in-line text differences (added, deleted and unchanged).

This is a fork of that project that changes multiple parts of the algorithm so that the differences returned hold a startIndex value. The main idea behind this change is to allow a quick retrieval of the difference as-is in the original document or in the edited document. The developer can use this value to collect a snippet of the contents surrounding the difference, using for example:
```java
String oldText;
String newText;
Diff deletedDiff;
Diff addedDiff;
int snippetOffset = 50;

// get a snippet of the deleted content along with some surrounding text for context
int start = deletedDiff.startIndex - snippetOffset;
int end = deletedDiff.startIndex + deletedDiff.length() + snippetOffset;
String deletedDiffSnippet = oldText.substring(start, end);

// get a snippet of the added content along with some surrounding text for context
start = addedDiff.startIndex - snippetOffset;
end = addedDiff.startIndex + addedDiff.length() + snippetOffset;
String addedDiffSnippet = newText.substring(start, end);
```

This has only been implemented for Java (my primary use-case). You can see this fork in use at https://github.com/vokter/vokter-core.

All of the required changes to add this index where made into a single commit, so if you wish to check the changes and adapt them to other languages that the original project supported, check here: TODO


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

