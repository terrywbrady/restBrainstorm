# Brainstorming for DSpace REST 

* [Data Flows](dataFlows.md) - Describe application scenarios (search/browse) and the sequence of calls to support them
* [Object Schemas](objectSchema.md) - Describe data elements for each object return type
* [Request Specs](requestSpec.md) - Describe the rest endpoints, required parameters and optional parameters

## Additional Thoughts
* Authentication
  * For ad-hoc REST clients developed outside of the standard UI, how will REST authentication work?  
  * How will stackable authentication be invoked?
* Admin Tasks
  * Could all admin tasks and command line tasks be collapsed into curation tasks (with parameters and output)
  * Could many custom admin endpoints be simplified if a corresponding curation task could be invoked?
