=========================
Python and MongoDB
=========================

This primarily refers to usage of the ``pymongo`` package, however, the
concepts apply to using MongoDB from Python in general. Interacting with
MongoDB from Python has a couple of easy traps to fall into, and this looks
at one in particular and how to avoid the pitfall via proper usage of indexes
and careful construction of queries.

When querying MongoDB in general, it will attempt to use indexes based on the
components of your query, *in the order you specify them*. That is, if you
construct a query that looks as follows:

.. code-block:: python

    docs = db.collection.find({"stuff": 1, "things": 0})

If you use that as the filter for a ``.find()`` call, MongoDB will look for a
compound index where the fields are specified in the order ``(stuff, things)``.
If a compound index exists with both fields but the ordering is instead
``(things, stuff)``, then the index *may not be used*! I have experienced a
number of situations where the query planner will select the correct index
despite providing the query fields in a different order, however, that behavior
should not be relied upon.

NOTE 1: make sure that you create compound indexes on your MongoDB collections
with the fields specified *in the order which you want to query them in* and
that you construct query filters using the same ordering as your indexes!

Great, so we understand that ordering is important on the MongoDB side of the
equation, but there's just one little problem. Almost all examples of using
a library like ``pymongo`` to interact with MongoDB from Python use plain old
``dict`` objects to construct query filters; the thing is, Python ``dict``
objects are inherently an unordered data structure and thus provide no
guarantee of maintaining any specific ordering. While that is not entirely true
for Python 3.6+ (but that is a whole different topic) I would still argue that
using the approach explained below conforms better to best practice and more
explicitly communicates the intent of what the code is doing.

If the filter only contains
a single field, then there won't be any issues because there aren't multiple
fields. However, as soon as you introduce multiple fields into a filter using
a normal ``dict``, the order in which they might be presented to MongoDB
becomes non-deterministic. This means that our example query might actually
be serialized at runtime to:

.. code-block:: json

    {"things": 0, "stuff": 1}

Which could prevent MongoDB from utilizing a compound index on
``(stuff, things)``. That might not be an issue on very small
collections, but try doing that on hundreds of thousands or millions of
documents and the queries will start taking orders of magnitude longer.

There are certain edge-cases with some versions of Python where depending on
whether hash randomization is enabled or not the ordering of ``dict``s may be
preserved (or at least deterministic), however, the point here is that things
like this **should not** ever be relied upon for ordering since the ``dict``
as a data structure provides no guarantees or ordering.

It is unfortunate that the pymongo documentation is not clearer on this point;
though it does mention it, you essentially have to read a section about a
method which takes a filter (like the collection
`find <http://api.mongodb.com/python/current/api/pymongo/collection.html#pymongo.collection.Collection.find>`_
method), and notice that the ``filter`` argument says:

    filter (optional): a SON object specifying elements which must be present
    for a document to be included in the result set

Well it says nothing about ``dict``... so what is a SON object? The quoted
description above provides no clickable link in the documentation, but if you
dig around a little more you can come across the
`Tools for working with SON an ordered mapping <http://api.mongodb.com/python/current/api/bson/son.html>`_
page about the ``bson.son`` module which defines ``SON`` objects, and says
(emphasis added by me):

    Regular dictionaries can be used instead of SON objects, **but not when
    the order of keys is important**. A SON object can be used just like a
    normal Python dictionary.

NOTE 2: now we see that filters are expected to be SON objects, or speaking
more broadly, ``dict`` objects *can* be used in *specific cases*, but as a
general rule **filters are expected to be an ordered mapping**.

Right, so ``pymongo`` actually expects an ordered mapping, which makes sense
based on the importance of ordering on the MongoDB side. How then do we ensure
that ordering is preserved for queries? There are effectively two options;
personally I've not found any compelling reasons to use ``bson.son.SON`` and
prefer to use the already-familiar option that is built right into Python,
``collections.OrderedDict``. ``OrderedDict`` acts almost exactly like a normal
``dict`` object, however, it also preserves the order in which keys were
inserted. Using this approach, our example query filter could instead be
constructed with:

.. code-block:: python

    from collections import OrderedDict

    query_filter = OrderedDict()
    query_filter['stuff'] = 1
    query_filter['things'] = 0

    docs = db.collection.find(query_filter)

It can also be built directly by utilizing the constructor but you have to
keep in mind that initializing data by *passing keyword arguments or another
dict object will not preserve ordering*. This is because ``OrderedDict`` can
only preserve what ordering it has access to, and neither kwargs nor a ``dict``
provide an order. Instead, you will need to pass it an *iterable* of some sort
(such as a list, tuple, or generator) of key-value pairs. Constructing the
example filter in this manner would look like:

.. code-block:: python

    from collections import OrderedDict

    query_filter = OrderedDict([('stuff', 1), ('things', 0)])

    docs = db.collection.find(query_filter)

NOTE 3: initializing it may not look as clean or pretty as a ``dict``, but you
should almost always use ``OrderedDict`` for performing MongoDB queries in
Python; you can initialize an ``OrderedDict`` properly by passing an iterable
of key-value pairs to the constructor. This will ensure that ordering is
preserved and ensure compound indexes with the same order will be utilized.
