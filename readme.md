# minifind

minifind is os.walk wrapper with predicates

# Install

```shell
pip install minifind
```

# Use

```python
from minifind import find, size_kb
```

Find have two modes of operation:

1) trigger callback on each matched file / directory

```python
def callback(name, path):
    print(path)

find("path/to/dir").for_each(callback)
```

2) collect matched items

```python
paths = find("path/to/dir").collect()
```

# Examples

Find source files of size 5kb+:

```python
def not_moc(name, path):
    return not name.startswith('moc_')

paths = find("D:\\dev").ext(".cpp", ".h").filter(not_moc).size(size_kb(5)).collect()
```

Find git dirs, but dont go deeper that two directories in:

```python
paths = find("D:\\dev").maxdepth(2).name('.git').collect()
```

# Predicates and modifiers

```
.files() - match files

.dirs() - match dirs

.ext(*patterns) - match file extensions

.name(*patterns) - match name patterns

.size(low, high) - match file size

.mtime(low, high) - match modification time

.filter(predicate) - match with your predicate

.maxdepth(n) - don't go deeper than n levels in.

.first(n) - stop after n matched files
```

# See also

[https://github.com/mugiseyebrows/pyfindlib](https://github.com/mugiseyebrows/pyfindlib)