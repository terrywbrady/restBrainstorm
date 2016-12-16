# Potential Call Sequences with REST Api

## Main Page Load
* Get breadcrumb data - returns nothing but a descriptive name at the top level
  * /api/core/hierarchy/ancestors/:node
    * :node = "top" or repo uuid  
* Get Welcome Message
  * /api/core/config/:prop-name
    * :prop-name = welcome
* Get List of Top Communities
  * /api/core/hierarchy/descendants/:node/:depth
    * :node = "top" or repo uuid
    * :depth = 1 to pull top level descendants
* Get Browse Options for whole repo
  * /api/discovery/:node/browse-options
    * :node = "top" or repo uuid
* Get Facet Options for whole repo
  * /api/discovery/:node/facets
    * :node = "top" or repo uuid
* Get Default Browse Option (likely recent items)
  * /api/browse/:node/:browse-mode
    * :node = "top" or repo uuid
    * :browse-mode = default - likely recent items
    * ?page - defaults to 0
    * ?size - defaults to default page size for node
* Get Available Actions for the Node (create community, edit community)
  * /api/actions/:node
    * :node = "top" or repo uuid

#### How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = "top" or repo uuid

***  
  
## Community-List Page
* Get List of Top Communities
  * /api/core/hierarchy/:node/:depth
    * :node = "top" or repo uuid
    * :depth = 0 to pull all levels of hierarchy
* Get Available Actions for the Node (create community, edit community)
  * /api/actions/:node
    * :node = "top" or repo uuid

***  

## Browse Community
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
* Get Browse Options for community
  * /api/discovery/:node/browse-options
    * :node = community uuid
* Get Facet Options for community
  * /api/discovery/:node/facets
    * :node = community uuid
* Get Default Browse Option (likely recent items)
  * /api/browse/:node/:mode
    * :node = community uuid
    * :mode = default - likely recent items
* Get Available Actions for the Node (create top community)
  * /api/actions/:node
    * :node = "top" or repo uuid

#### How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = community uuid

***  

## Browse Community
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
* Get Browse Options for community
  * /api/discovery/:node/browse-options
    * :node = community uuid
* Get Facet Options for community
  * /api/discovery/:node/facets
    * :node = community uuid
* Get Default Browse Option (likely recent items)
  * /api/browse/:node/:mode
    * :node = community uuid
    * :mode = default - likely recent items
    * ?page - defaults to 0
    * ?size - defaults to default page size for node
* Get Available Actions for the Node (create sub-community, create collection, edit community)
  * /api/actions/:node
    * :node = "top" or repo uuid

#### How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = community uuid
