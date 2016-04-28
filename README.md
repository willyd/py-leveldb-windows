# Python leveldb wrapper for [Caffe](http://caffe.berkeleyvision.org/) & [Caffe-builder](https://github.com/willyd/caffe-builder) under Windows
Helper project to compile Python leveldb wrapper under Windows using CMake.

C++ libraries (leveldb and its dependencies) will be resolved from [Caffe-builder](https://github.com/willyd/caffe-builder)'s install tree.

## Usage
1. Setup [caffe-builder](https://github.com/willyd/caffe-builder/blob/master/README.md)
2. Run this command
```
ninja pyleveldb 
```
this should download, build and install pyleveldb and its dependencies.
3. Copy `%buildir%/install/leveldb/bin/leveldb.pyd` and the other in the same dlls to `%PYTHON_PATH%/Lib/site-packages`

4. Run `python ./test-py-leveldb.py`. If everything is ok, you will get `hello world` response and a folder named `db`.
(Test is taken from https://github.com/happynear/py-leveldb-windows)

