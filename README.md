# Osmread

**See Fork Notes before using**

Osmread is a simple library for reading OpenStreetMap data files in Python. It
supports XML and PBF file formats as inputs. It is not designed for fast
processing of big planet dumps but can be used for simple processing of smaller
files such as regional extracts.

If you need fast processing of large files look at 
[imposm.parser][imposm.parser] library.


## Fork Notes
* The implementation (that was awesome) of PBF support is removed to play nice with Jython
* The dependency on `lxml` was replaced with the built in `ElementTree`, again for Jython compatability (no C extensions)


## Installation

Simply run `setup.py` or use `pip` or `easy_install`.

    $ python setup.py install


## Example usage

    from osmread import parse_file, Way

    highway_count = 0
    for entity in parse_file('foo.osm.bz2'):
        if isinstance(entity, Way) and 'highway' in entity.tags:
            highway_count += 1

    print("%d highways found" % highway_count)

All `Node`, `Way` and `Relation` instances have `id`, `version`, `changeset`,
`timestamp`, `uid` and `tags` attributes. Node coordinates stored in `lon` and
`lat`. Way nodes stored in `nodes`, relation members in `members`.

Relation members are array of tuples (`role`, `class`, `id`), where `class` is
`Node`, `Way` or `Relation`.

## PBF implementation note

**PBF support is totally removed in this fork.** WTF? Jython compatability (due to class size restrictions).

~~This library uses very slow protobuf implementation - pure python 
[protobuf][protobuf] library. As a result parsing PBF files is slower than XML.~~
~~This may change in future versions.~~


[imposm.parser]: http://pypi.python.org/pypi/imposm.parser
~~[protobuf]: http://pypi.python.org/pypi/protobuf~~
