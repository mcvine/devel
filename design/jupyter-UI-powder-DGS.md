# jupyter user interfaces for mcvine simulations of powder DGS experiments

* beam simulation
* sample creation
* scattering simulation and preliminary reduction

## Beam simulation
* Select instrument
* sim parameters
* choose output dir
* confirm and run

## Sample creation
* name
* chemical formula
* a,b,c, alpha, beta, gamma
* excitation
  * type
  * config
* shape
  * type
  * config

This creates a yaml file

## Scattering sim
* Choose beam directory
* Choose sample directory
* Choose work directory
* Choose simulation parameters
* Generate the simulate folder, and give instructions


## Implementation

* Interface: https://github.com/mcvine/ui/tree/master/ui/jupyter 
* Example notebooks: https://github.com/mcvine/training/tree/master/jui
* yaml schema: https://github.com/mcvine/devel/blob/master/design/sampleassembly-scaffolding.md
* Kernels: https://github.com/mcvine/workflow/tree/master/workflow/sampleassembly/scaffolding

### Principles
* More detailed help for forms/parameters etc are wiki pages at https://github.com/mcvine/ui/wiki. They are referred to by help text in the interface. See for example: [DGS beam form help referred here]( https://github.com/mcvine/ui/blob/97ae5b3c5816473346fee32592ae6b860a7df506/ui/jupyter/beam.py#L41)

