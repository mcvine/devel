# Instrument simulation pipeline driver

The top-level simulation is a linear pipeline.
The simulation pipeline can now be driven in two main ways

* by [mcni.simulate](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/__init__.py#L27),
  which works with "vanilla" components 
  (subclasses of [AbstractComponent](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/AbstractComponent.py))
* by [pyre instrument](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/Instrument.py), 
  which contains a sequence of pyre components 
  (subclasses of [pyre AbstracComponent](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/AbstractComponent.py))


## [mcni.simulate](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/__init__.py#L27)

It is a simmple driver that given a list of components, run a neutron buffer through them

## [pyre instrument](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/Instrument.py)

It uses pyre machinery. The components are registered as pyre facilities in Instrument's inventory. In the `main` function of Instrument, `mcni.simulate` is called to actually run the simulation.

The pyre.Instrument also provides machinery to 
* split the full simulation load into a bunch of smaller simulations. This way, only a relatively small "neutron buffer" is needed to hold neutrons in memory. It runs a loop to make sure the full simulation load is carried out.
* do parallel simulation. This means (almost) evenly splitting the simulation load into available simulation cores. This is done by MPI
