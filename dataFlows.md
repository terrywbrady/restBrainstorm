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

## Get Context for a Repository/Community/Collection Page
* Get Context Options for Current Node
  * GET /api/node-context/:node 
    * :node = "top" or repo uuid
    * :depth 
      * 1 to pull top level descendants
      * 0 to pull all descendants
    * returns [NodeContext](objectSchema.md#nodecontext) 
  * This will load all of the relevant resources for a hierarchy node
    * Get breadcrumb data - returns nothing but a descriptive name at the top level
      * GET /api/core/hierarchy/ancestors/:node
        * :node = "top" or repo uuid  
        * returns Array of [MinimalDSO](objectSchema.md#minimaldso)
    * Get List of Top Communities
      * GET /api/core/hierarchy/descendants/:node/:depth
        * :node = "top" or repo uuid
        * :depth 
          * 1 to pull top level descendants
          * 0 to pull all descendants
        * returns [Hierarchy](objectSchema.md#hierarchy) containing only top level communities
    * Get Browse Options for whole repo
      * GET /api/discovery/:node/browse-options
        * :node = "top" or repo uuid
        * returns Array of [Option](objectSchema.md#option)
    * Get Facet Options for whole repo
      * GET /api/discovery/:node/facets
        * :node = "top" or repo uuid
        * returns Array of [Facet](objectSchema.md#facet)
    * Get Available Actions for the Node (create community)
      * GET /api/actions/:node
        * :node = "top" or repo uuid
        * returns Array of [Action](objectSchema.md#action)

## Main Page Load
* Browse to the repository landing page, retrieve relevant resources
* Get NodeContext for the entire repository (only top level communities)
  * GET /api/node-context/:node
    * :node: "top" or repo uuid  
    * :depth: 1 to pull only top level communities
    * returns [NodeContext](objectSchema.md#nodecontext)
* Get Welcome Message
  * GET /api/core/config/:prop-group
    * :prop-group = ui
    * :prop-name = welcome
    * returns [Property](objectSchema.md#property)
* Get Items per Default Browse Option (likely recent items) - retrieves relevant (accessible) items in a logical order
  * GET /api/browse/items/:node/:browse-mode
    * :node = "top" or repo uuid
    * :browse-mode = default - likely recent items
    * ?page - defaults to 0
    * ?size - defaults to default page size for node
    * returns array of [Item](objectSchema.md#item)

***  
  
## Community-List Page
* Get List of Top Communities
* Get NodeContext for the entire repository
  * GET /api/node-context/:node
    * :node: "top" or repo uuid  
    * :depth: 0 to pull full hierarchy
    * returns [NodeContext](objectSchema.md#nodecontext)

***  

## Browse Community/Collection
* Browse a community or collection page, retrieve relevant resources
* Get core metadata data for community/collection (name, handle)
  * GET /api/core/dso/:node
    * :node = community/collection uuid
    * returns [MinimalDSO](objectSchema.md#minimaldso)
* Get descriptive metadata data for community/collection
  * GET /api/core/metadata/:node
    * :node = community/collection uuid
    * returns Array of [Metadata](objectSchema.md#metadata)
* Get NodeContext for the community/collection
  * GET /api/node-context/:node
    * :node: "top" or repo uuid  
    * :depth: 0 to pull all community descendants
    * returns [NodeContext](objectSchema.md#nodecontext)
* Get Items per Default Browse Option (likely recent items) - retrieves relevant (accessible) items in a logical order
  * GET /api/browse/items/:node/:browse-mode
    * :node = "top" or repo uuid
    * :browse-mode = default - likely recent items
    * ?page - defaults to 0
    * ?size - defaults to default page size for node
    * returns array of [Item](objectSchema.md#item)

***  

## Browse Item
* Browse to an item page
* Get core metadata data for item (name, handle)
  * GET /api/core/dso/:node
    * :node = item uuid
    * returns [MinimalDSO](objectSchema.md#minimaldso)
* Get descriptive metadata data for item
  * GET /api/core/metadata/:node
    * :node = item uuid
    * returns Array of [Metadata](objectSchema.md#metadata)
* Get breadcrumb data
  * GET /api/core/hierarchy/ancestors/:node
    * :node = item uuid
    * returns Array of [MinimalDSO](objectSchema.md#minimaldso)
* Get bitstreams
  * GET /api/core/bitstreams/:node/:bundle/:num
    * :node = item uuid
    * :bundle - defaults to ORIGINAL
    * :depth = 1 to pull primary bitstream, 0 to pull all, n to paginate
    * ?associated-bundles - defaults to THUMBNAIL - a link to associated bitstreams will be returned with an original bitstream
    * returns array of [Bitstream](objectSchema.md#bitstream)
* Get Related Items
  * GET /api/discovery/:node/related-items
    * :node = item uuid
    * returns array of [Item](objectSchema.md#item)
* Get Available Actions for the Node (edit item, usage stats)
  * GET /api/actions/:node
    * :node = "top" or repo uuid
    * returns Array of [Action](objectSchema.md#action)

***  

## Search Entire Repository / Community / Collection
* Search repository for items
  * POST /api/discovery/:node/search
    * :node = "top" or repo uuid or comm/coll uuid
    * ?page = page number
    * ?size = page size
    * ?sort-mode = choose from available sort options, the default sort will be used if not specified
    * POST Content - solr query for "search" repo, may include advanced search text and facet values
  * This call will load all of the relevant resources which could be called individually
    * Get breadcrumb data
      * GET /api/core/hierarchy/ancestors/:node
        * "top" or repo uuid or comm/coll uuid
        * returns Array of [MinimalDSO](objectSchema.md#minimaldso)
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
    * Return the list of available advanced search filters for a particular node
      * GET /api/discovery/:node/search-filters
        * :node = "top" or repo uuid or comm/coll uuid
    * Assumption: Discovery service will return core metadata for each item
    * Get bitstreams for search results (iterate over results)
      * GET /api/core/bitstreams/:node/:bundle/:num
        * :node = dso uuid
        * :bundle - defaults to THUMBNAIL
        * :depth = 1 to pull primary bitstream
    * Get Available Actions for the Node (edit item, usage stats)
      * GET /api/actions/:node
        * :node = "top" or repo uuid
        * returns Array of [Action](objectSchema.md#action)

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

## Edit Collection Content Source

***

## Curate Collection

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

## Administer

* Administer people
* Administer groups
* Administer policies
* Administer schema registry
* Administer metadata field registry
* Administer format registry
* Administer content
  * Initiate bulk metadata edit
  * Initiate bulk ingest
  * Find special items
    * Withdrawn items
    * Private items
    * (Other special filters to plug in)
    * Metadata query?
* Control panel View
* Configurable Workflows checks like Sherpa
