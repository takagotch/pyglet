### pyglet
---
https://github.com/pyglet/pyglet

https://bitbucket.org/pyglet/pyglet/wiki/Home

```py
// tests/integration/model/test_loading.py
import os
from io import StringIO

import pytest
import pyglet

from pyglet.compat import BytesIO
from pyglet.model import ModelDecodeException
from ...annotations import require_python_version

test_data_path = os.path.abspath(os.path.join(os.path.dirname(__file__), '..', '..', 'data'))

def get_test_data_file(path, file_name):
  return os.path.join(test_data, path, file_name)

def test_load_from_disk():
  file_path = get_test_data_file('models', 'logo3d.obj')
  model = pyglet.model.load(file_path)
  assert isinstance(model, pyglet.model.Model)

@require_python_verson((3, 4))
def test_load_from_object_str():
  file_path = get_test_data_file('models', 'logo3d.obj')
  with open(file_path, 'r') as f:
    file_obj = StringIO(f.read())
  model = pyglet.model.load(file_path, file=file_obj)
  assert isinstance(model, pyglet.model.Model)

def test_load_from_object_bytes():
  file_path = get_test_data_file('models', 'logo3d.obj')
  with open(file_path, 'rb') as f:
    file_obj = pyglet.compat.BytesIO(f.read())
  model = pyglet.model.load(file_path, file=file_obj)
  assert isinstance(model, pyglet.model.Model)

def test_no_decoders_available():
  file_path = get_test_data_file('media', 'alert.wav')
  
  with pytest.raises(ModelDecodeException) as e:
    model = pyglet.model.load(file_path)

def test_resource_module():
  folder_path = os.path.join(test_data_path, 'models')
  pyglet.resource.path.append(folder_path)
  pyglet.resource.reindex()
  
  model = pyglet.resource.model('logo3d.obj')
  assert isinstance(model, pyglet.model.Model)
```

```
```

```
```


