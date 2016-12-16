# Potential Call Sequences with REST Api

### Main Page Load
* Get Welcome Message
  * /api/core/config/:prop-name
    * :prop-name = welcome
* Get List of Top Communities
  * /api/core/hierarchy/descendants/:node/:depth
    * :node = "top" or repo uuid
    * :depth = 1 to pull top level descendants
* Get Recent Items
  * /api/discovery/:node/recent-items
    * :node = "top" or repo uuid
* Get Browse Options for whole repo
  * /api/discovery/:node/browse-options
    * :node = "top" or repo uuid
* Get Browse Options for whole repo
  * /api/discovery/:node/facets
    * :node = "top" or repo uuid
* How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = "top" or repo uuid
    * ?expand=browse - return all relevant components to support browse
  
### Community-List Page
* Get List of Top Communities
  * /api/core/hierarchy/:node/:depth
    * :node = "top" or repo uuid
    * :depth = 0 to pull all levels of hierarchy

### Browse Community
* Get core metadata data for community (name, handle)
  * /api/core/community/:node
    * :node = community uuid
* Get descriptive metadata data for community
  * /api/core/metadata/:node
    * :node = community uuid
* Get breadcrumb data
  * /api/core/hierarchy/ancestors/:node
    * :node = community uuid
* Get descendant subcommunities and collections
  * /api/core/hierarchy/descendants/:node/:depth
    * :node = community uuid
    * :depth = 1 to pull direct subcommunity and collection descendants
