# Instrument simulation pipeline driver

The top-level simulation is a linear pipeline.
The simulation pipeline can now be driven in two main ways

* by [mcni.simulate](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/__init__.py#L27),
  which works with "vanilla" components 
  (subclasses of [AbstractComponent](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/AbstractComponent.py))
* by [pyre instrument](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/Instrument.py), 
  which contains a sequence of pyre components 
  (subclasses of [pyre AbstracComponent](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/AbstractComponent.py))
