---
description: Cheatsheet of gsutil commands
---

# 📔 gsutil cheatsheet



| Command                                            | Description                                 | Notes                                                                                                                      |
| -------------------------------------------------- | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| gsutil mb -l $LOCATION gs://$DEVSHELL\_PROJECT\_ID | create bucket named after unique project ID | <ul><li>$LOCATION env var must be declared first</li><li>$DEVSHELL... env var already exists with the project id</li></ul> |
| `gsutil cp <loc://path/file.png> <new-file.png>`   | Copy file                                   |                                                                                                                            |
| gsutil mb gs://\<bucket-name>                      | Make a bucket                               |                                                                                                                            |
