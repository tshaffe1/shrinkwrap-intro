Shrinkwrap: Creating HPC Containers
===================================

Material for the
[talk](https://indico.cern.ch/event/757415/contributions/3421537/)
at the
[CernVM Workshop 2019](https://indico.cern.ch/e/cvm19).


- What is Shrinkwrap?
- Compared to UnCVMFS and rsync
- Use Cases
- Downloading and Building **(Nick)**
- Setup **(Nick)**
  + Config files
  + Keys
- Specifications **(Nick)**
  + Selecting Revisions
  + Full Repo (example, and simple exclusions)
  + Hand-written specs
  + Tracing (support in FUSE module, Parrot)
- Shrinkwrap Usage **(Tim)**
  + Basic invocation
  + Rough Performance
  + Efficient Updates
- Building Containers **(Tim)**
  + SquashFS
  + Docker
  + Singularity
- Managing Images **(Tim)**
  + Full-repo copies
  + Per-job creation
  + Shared images
