.. _core-walkthrough:

What is Ray Core?
=================

.. toctree::
    :maxdepth: 1
    :hidden:

    Key Concepts <key-concepts>
    User Guides <user-guide>
    Examples <examples/overview>
    api/index


Ray Core provides a small number of core primitives (i.e., tasks, actors, objects) for building and scaling distributed applications. Below we'll walk through simple examples that show you how to turn your functions and classes easily into Ray tasks and actors, and how to work with Ray objects.

.. note::

    Ray has introduced an experimental API for high-performance workloads that is
    especially well suited for applications using multiple GPUs.
    See :ref:`Ray Compiled Graph <ray-compiled-graph>` for more details.

Getting Started
---------------

To get started, install Ray via ``pip install -U ray``. See :ref:`Installing Ray <installation>` for more installation options. The following few sections will walk through the basics of using Ray Core.

The first step is to import and initialize Ray:

.. literalinclude:: doc_code/getting_started.py
    :language: python
    :start-after: __starting_ray_start__
    :end-before: __starting_ray_end__

.. note::

  In recent versions of Ray (>=1.5), ``ray.init()`` is automatically called on the first use of a Ray remote API.

Running a Task
--------------

Ray lets you run functions as remote tasks in the cluster. To do this, you decorate your function with ``@ray.remote`` to declare that you want to run this function remotely.
Then, you call that function with ``.remote()`` instead of calling it normally.
This remote call returns a future, a so-called Ray *object reference*, that you can then fetch with ``ray.get``:

.. literalinclude:: doc_code/getting_started.py
    :language: python
    :start-after: __running_task_start__
    :end-before: __running_task_end__

Calling an Actor
----------------

Ray provides actors to allow you to parallelize computation across multiple actor instances. When you instantiate a class that is a Ray actor, Ray will start a remote instance of that class in the cluster. This actor can then execute remote method calls and maintain its own internal state:

.. literalinclude:: doc_code/getting_started.py
    :language: python
    :start-after: __calling_actor_start__
    :end-before: __calling_actor_end__

The above covers very basic actor usage. For a more in-depth example, including using both tasks and actors together, check out :ref:`monte-carlo-pi`.

Passing an Object
-----------------

As seen above, Ray stores task and actor call results in its :ref:`distributed object store <objects-in-ray>`, returning *object references* that can be later retrieved. Object references can also be created explicitly via ``ray.put``, and object references can be passed to tasks as substitutes for argument values:

.. literalinclude:: doc_code/getting_started.py
    :language: python
    :start-after: __passing_object_start__
    :end-before: __passing_object_end__

Next Steps
----------

.. tip:: To check how your application is doing, you can use the :ref:`Ray dashboard <observability-getting-started>`.

Ray's key primitives are simple, but can be composed together to express almost any kind of distributed computation.
Learn more about Ray's :ref:`key concepts <core-key-concepts>` with the following user guides:

.. grid:: 1 2 3 3
    :gutter: 1
    :class-container: container pb-3


    .. grid-item-card::
        :img-top: /images/tasks.png
        :class-img-top: pt-2 w-75 d-block mx-auto fixed-height-img

        .. button-ref:: ray-remote-functions

            Using remote functions (Tasks)

    .. grid-item-card::
        :img-top: /images/actors.png
        :class-img-top: pt-2 w-75 d-block mx-auto fixed-height-img

        .. button-ref:: ray-remote-classes

            Using remote classes (Actors)

    .. grid-item-card::
        :img-top: /images/objects.png
        :class-img-top: pt-2 w-75 d-block mx-auto fixed-height-img

        .. button-ref:: objects-in-ray

            Working with Ray Objects
