# Potential Call Sequences with REST Api

## Object References
This documentation presumes uuid will be the primary key for api calls.

* /api/_action_/:node

It could be attractive to support both uuids and handles in API calls.

Why? 
* Handles are more intuitive to new users.  
* Handles may be more accessible in an ajax add-on.  
* Handles are preserved in AIP export/import - could allow for test re-use

Alternate options for access
* /api/_action_/uuid/:uuid
* /api/_cation_/handle/:handle-prefix/:handle_suffix

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

## Browse Community/Collection
* Get core metadata data for community/collection (name, handle)
  * /api/core/dso/:node
    * :node = community/collection uuid
* Get descriptive metadata data for community/collection
  * /api/core/metadata/:node
    * :node = community/collection uuid
* Get breadcrumb data
  * /api/core/hierarchy/ancestors/:node
    * :node = community/collection uuid
* Get descendant subcommunities and collections (returns nothing for collections)
  * /api/core/hierarchy/descendants/:node/:depth
    * :node = community/collection uuid
    * :depth = 1 to pull direct subcommunity and collection descendants
* Get Browse Options for community/collection
  * /api/discovery/:node/browse-options
    * :node = community/collection uuid
* Get Facet Options for community/collection
  * /api/discovery/:node/facets
    * :node = community/collection uuid
* Get Default Browse Option (likely recent items)
  * /api/browse/:node/:mode
    * :node = community/collection uuid
    * :mode = default - likely recent items
* Get Available Actions for the Node (create collection, edit comm/coll, submit item)
  * /api/actions/:node
    * :node = "top" or repo uuid

#### How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = community/collection uuid

***  

## Browse Item
* Get core metadata data for item (name, handle)
  * /api/core/dso/:node
    * :node = item uuid
* Get descriptive metadata data for item
  * /api/core/metadata/:node
    * :node = item uuid
* Get breadcrumb data
  * /api/core/hierarchy/ancestors/:node
    * :node = item uuid
* Get bitstreams
  * /api/core/bitstreams/:node/:bundle/:num
    * :node = item uuid
    * :bundle - defaults to ORIGINAL
    * :depth = 1 to pull primary bitstream, 0 to pull all, n to paginate
    * ?associated-bundles - defaults to THUMBNAIL - a link to associated bitstreams will be returned with an original bitstream
* Get Related Items
  * /api/discovery/:node/related-items
    * :node = item uuid
* Get Available Actions for the Node (edit item, usage stats)
  * /api/actions/:node
    * :node = "top" or repo uuid

#### How to bundle the information above?
  * /api/core/hierarchy/browse/:node
    * :node = item uuid

***  

## Search Entire Repository
* Get breadcrumb data
  * /api/core/hierarchy/ancestors/:node
    * "top" or repo uuid
* Get Browse Options for whole repo
  * /api/discovery/:node/browse-options
    * :node = "top" or repo uuid
* Search repository for items
  * /api/discovery/:node/search
    * :node = "top" or repo uuid
    * ?query = solr query for "search" repo
    * ?page = page number
    * ?size = page size
    * ?sort-mode = choose from available sort options, the default sort will be used if not specified
* Get Facet Options related to search hits
  * /api/discovery/:node/search/facets
    * :node = community/collection uuid
    * ?query = solr query for "search" repo
* Return the list of available sort modes for a particular node
  * /api/discovery/:node/sort-modes
    * :node = "top" or repo uuid
* Retrun the list of available advanced search filters for a particular node
  * /api/discovery/:node/search-filters
    * :node = "top" or repo uuid
* Assumption: Discovery service will return core metadata for each item
* Get bitstreams for search results (iterate over results)
  * /api/core/bitstreams/:node/:bundle/:num
    * :node = dso uuid
    * :bundle - defaults to THUMBNAIL
    * :depth = 1 to pull primary bitstream
    
  
