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
* do parallel simulation. This means (almost) evenly splitting the simulation load into available simulation cores. This is done by MPI
* split the full simulation load into a bunch of smaller simulations. This way, only a relatively small "neutron buffer" is needed to hold neutrons in memory. It runs a loop to make sure the full simulation load is carried out. This loop happens inside each node (in-node-loop).

During simulation, each step in a in-node-loop for each node will run inside a specific directory: `rank{core_id}-step{iteration_id}` (e.g. `rank3-step5`).

After simulation is done, a component can write out a script in a specific directory to merge the results from all these directories together. For example, all histogram-based monitor component inherits
[this method](https://github.com/mcvine/mcvine/blob/1807ea3c1ac7bfb4450e6e89b249e8a4304317ef/packages/mcni/python/mcni/components/HistogramBasedMonitorMixin.py#L74). See also: [DetectorSystemFromXml](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mccomponents/python/mccomponents/pyre_support/components/DetectorSystemFromXml.py#L89), [NeutronToStorage](https://github.com/mcvine/mcvine/blob/42b190cb3f67e8018464f5029dfb69f373cb6649/packages/mcni/python/mcni/pyre_components/NeutronToStorage.py#L63)


## [mcvine.InstrumentBuilder](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcvine/python/mcvine/applications/InstrumentBuilder.py)

`mcvine.InstrumentBuilder` wraps the [pyre instrument](https://github.com/mcvine/mcvine/blob/62369e564a491dcfd378475084c54b81e022a461/packages/mcni/python/mcni/pyre_support/Instrument.py) and runs the post-processing scripts written out by the components in the pipeline.


