.. _define-namespacing:

Namespacing
-----------

While most of the classes and code in a plugin will automatically be namespaced by virtue of modules
in Python, the REST API is a different story due to endpoints. This is especially true with
resources that extend classes provided by pulpcore.

For exmaple, a plugin writer might initially be tempted to define their content viewset like so:

.. code-block:: python

    class PackageViewSet(ContentViewSet):
        endpoint_name = 'packages'


However, another plugin might define a packages content endpoint too so to avoid this, one should
namespace their endpoints. Suppose you had a plugin called 'foobar', you can define the following:

.. code-block:: python

    class PackageViewSet(ContentViewSet):
        endpoint_name = 'foobar/packages'


It's also possible that if your plugin has a single content type that matches the name of your
plugin, you could just define your viewset like so:

.. code-block:: python

    class FoobarViewSet(ContentViewSet):
        endpoint_name = 'foobar'


However, we recommend against this pattern as it makes defining more content types in the future
impossible without introducing breaking changes. Instead use namespaced nesting described above.

In addition to :class:`~pulpcore.app.models.Content` endpoints, namespacing should also be
considered when defining endpoints for :class:`~pulpcore.app.models.Publisher`s and
:class:`~pulpcore.app.models.Remote`s.
