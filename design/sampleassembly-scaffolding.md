
The idea is that we start with a relatively simple representation of the sample (and sample environment), which can be serialized using yaml, and build the sample assembly (xml and relevant files).

Here is an example of the yaml file
```
name: KVO
chemical_formula: K2V3O8
lattice: 
 constants: 8.87, 8.87, 5.2, 90, 90, 90
 basis_vectors:
  - 8.87, 0, 0
  - 0, 8.87, 0
  - 0, 0, 5.2
excitation:
 type: spinwave
 E_Q: 2.563*sqrt(1-(cos(h*pi)*cos(k*pi))**2)
 S_Q: 1
 Emax: 3
orientation:
 u: 1, 0, 0
 v: 0, 1, 0
shape: |
       <rotation angles="90.*deg,0*deg,0*deg">
         <block width="4.6*cm" height="4.6*cm" thickness="2.3/4*cm"/>
       </rotation>
temperature: 300*K
```

The yaml file can be loaded by 

```from mcvine.workflow.sample import loadSampleYml
sample = loadSampleYml(yaml_path)
```

Then a sample assembly can be created from the sample

```
from mcvine.workflow.singlextal.scaffolding import createSampleAssembly
createSampleAssembly(outdir, sample)
```

To include sample environment, we should also support `createSampleAssembly(outdir, sample, sample_environment, ...)

