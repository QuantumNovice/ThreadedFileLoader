# Threaded File Loader

<a href='https://github.com/QuantumNovice/ThreadedFileLoader'> Github: ThreadedFileLoader</a>

Multithreaded Python package for faster file loading in machine learning.

# Installation
`pip install ThreadedFileLoader`

# Usage:
## Loading Image Files:
```python
from ThreadedFileLoader.ThreadedFileLoader import *

instance = ThreadedImageLoader("path_to_/*.jpg")
instance.start_loading()
images = instance.loaded_objects
print(len(images))
print(images[0].shape)
```

## Loading Text Files:
```python
from ThreadedFileLoader.ThreadedFileLoader import *

instance = ThreadedTextLoader("path_to_/*.txt")
instance.start_loading()
images = instance.loaded_objects
```

## Loading Custom File Formats
Threaded FileLoader can load different file types.
This examples shows how the `ThreadedTextLoader` class
overloads the `ThreadedFileLoader` class to load text files.

```python
from ThreadedFileLoader.ThreadedFileLoader import *

class ThreadedTextLoader(ThreadedFileLoader):
    def object_loader(self, path):
      with open(path) as afile:
        data = afile.readlines()
        return data

instance = ThreadedTextLoader("path_to_/*.txt")
instance.start_loading()
texts = instance.loaded_objects
```

# Machine Learning Example
## Loading Dataset


```Python
import numpy as np

from ThreadedFileLoader.ThreadedFileLoader import *
from sklearn.cluster import KMeans


instance = ThreadedImageLoader("path_to_dataset/*.jpg")
instance.start_loading()
images = instance.loaded_objects
images = np.array(images)
images = images.reshape(len(images), -1)

kmeans = KMeans(n_clusters=10, random_state=0).fit(images)

print(kmeans.labels_)

```
