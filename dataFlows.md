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
* Browse to the repository landing page, retrieve relevant resources
  * GET /api/browse/page/:node
      * :node = "top" or repo uuid  
  * This call will load all of the relevant resources which could be called individually
    * Get breadcrumb data - returns nothing but a descriptive name at the top level
      * GET /api/core/hierarchy/ancestors/:node
        * :node = "top" or repo uuid  
    * Get Welcome Message
      * GET /api/core/config/:prop-group
        * :prop-group = ui
        * :prop-name = welcome
    * Get List of Top Communities
      * GET /api/core/hierarchy/descendants/:node/:depth
        * :node = "top" or repo uuid
        * :depth = 1 to pull top level descendants
    * Get Browse Options for whole repo
      * GET /api/discovery/:node/browse-options
        * :node = "top" or repo uuid
    * Get Facet Options for whole repo
      * GET /api/discovery/:node/facets
        * :node = "top" or repo uuid
    * Get Default Browse Option (likely recent items) - retrieves relevant (accessible) items in a logical order
      * GET /api/browse/items/:node/:browse-mode
        * :node = "top" or repo uuid
        * :browse-mode = default - likely recent items
        * ?page - defaults to 0
        * ?size - defaults to default page size for node
    * Get Available Actions for the Node (create community)
      * GET /api/actions/:node
        * :node = "top" or repo uuid

***  
  
## Community-List Page
* Get List of Top Communities
  * GET /api/core/hierarchy/:node/:depth
    * :node = "top" or repo uuid
    * :depth = 0 to pull all levels of hierarchy
* Get Available Actions for the Node (create community, edit community)
  * GET /api/actions/:node
    * :node = "top" or repo uuid

***  

## Browse Community/Collection
* Browse to the repository landing page, retrieve relevant resources
  * GET /api/browse/page/:node
      * :node = community/collection uuid
  * This call will load all of the relevant resources which could be called individually
    * Get core metadata data for community/collection (name, handle)
      * GET /api/core/dso/:node
        * :node = community/collection uuid
    * Get descriptive metadata data for community/collection
      * GET /api/core/metadata/:node
        * :node = community/collection uuid
    * Get breadcrumb data
      * GET /api/core/hierarchy/ancestors/:node
        * :node = community/collection uuid
    * Get descendant subcommunities and collections (returns nothing for collections)
      * GET /api/core/hierarchy/descendants/:node/:depth
        * :node = community/collection uuid
        * :depth = 1 to pull direct subcommunity and collection descendants
    * Get Browse Options for community/collection
      * GET /api/discovery/:node/browse-options
        * :node = community/collection uuid
    * Get Facet Options for community/collection
      * GET /api/discovery/:node/facets
        * :node = community/collection uuid
    * Get Default Browse Option (likely recent items) - retrieves relevant items in a logical order
      * GET /api/browse/items/:node/:mode
        * :node = community/collection uuid
        * :mode = default - likely recent items
    * Get Available Actions for the Node (create collection, edit comm/coll, submit item)
      * GET /api/actions/:node
        * :node = "top" or repo uuid

***  

## Browse Item
* Browse to the repository landing page, retrieve relevant resources
  * GET /api/browse/page/:node
      * :node = item uuid
  * This call will load all of the relevant resources which could be called individually
    * Get core metadata data for item (name, handle)
      * GET /api/core/dso/:node
        * :node = item uuid
    * Get descriptive metadata data for item
      * GET /api/core/metadata/:node
        * :node = item uuid
    * Get breadcrumb data
      * GET /api/core/hierarchy/ancestors/:node
        * :node = item uuid
    * Get bitstreams
      * GET /api/core/bitstreams/:node/:bundle/:num
        * :node = item uuid
        * :bundle - defaults to ORIGINAL
        * :depth = 1 to pull primary bitstream, 0 to pull all, n to paginate
        * ?associated-bundles - defaults to THUMBNAIL - a link to associated bitstreams will be returned with an original bitstream
    * Get Related Items
      * GET /api/discovery/:node/related-items
        * :node = item uuid
    * Get Available Actions for the Node (edit item, usage stats)
      * GET /api/actions/:node
        * :node = "top" or repo uuid

***  

## Search Entire Repository / Community / Collection
* Search repository for items
  * POST /api/discovery/:node/search
    * :node = "top" or repo uuid or comm/coll uuid
    * ?page = page number
    * ?size = page size
    * ?sort-mode = choose from available sort options, the default sort will be used if not specified
    * POST Content - solr query for "search" repo, may include advanced search text and facet values
* Get breadcrumb data
  * GET /api/core/hierarchy/ancestors/:node
    * "top" or repo uuid or comm/coll uuid
* Get Browse Options for whole repo / comm / coll
  * GET /api/discovery/:node/browse-options
    * :node = "top" or repo uuid or comm/coll uuid
* Get Facet Options related to search hits
  * GET /api/discovery/:node/search/facets
    * :node = "top" or repo uuid or comm/coll uuid
    * ?query = solr query for "search" repo
* Return the list of available sort modes for a particular node
  * GET /api/discovery/:node/sort-modes
    * :node = "top" or repo uuid or comm/coll uuid
* Retrun the list of available advanced search filters for a particular node
  * GET /api/discovery/:node/search-filters
    * :node = "top" or repo uuid or comm/coll uuid
* Assumption: Discovery service will return core metadata for each item
* Get bitstreams for search results (iterate over results)
  * GET /api/core/bitstreams/:node/:bundle/:num
    * :node = dso uuid
    * :bundle - defaults to THUMBNAIL
    * :depth = 1 to pull primary bitstream

***  

## Select Facet
* See Search Entire Repository / Community / Collection
  * This option updates the POST data content

***  

## Download Bitstream 

***  

## Browse to inaccessible community/collection

***

## Browse to inaccessible item

***

## Attempt to Download Bitstream (inaccessible to user)
  
***

## Create Community

***

## Edit Community

***

## Edit Community Policies

***

## Create Collection

***

## Edit Collection Metadata

***

## Edit Collection Policies

***

## Submit New Item to A Collection

***

## Edit Item in Workflow

***

## Review Item in Workflow

***

## Cancel Item Workflow

***

## Edit Item Metadata

***

## Modify Item Bitstreams

***

## Alter Item Collection Ownership

***

## Alter Item Access Rigths

***

## Alter Bitstream Access Rigths with an Item

***
