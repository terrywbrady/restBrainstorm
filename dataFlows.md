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
    * Payload: solr query for "search" repo, may include advanced search text and facet values
    * returns [NodeContext](objectSchema.md#nodecontext) with search results and facets tailored to hits
  
***  

## Select Facet
* See Search Entire Repository / Community / Collection
  * This option updates the POST data content
  * returns [NodeContext](objectSchema.md#nodecontext) with search results and facets tailored to hits

***  

## Download Bitstream 
  * GET /api/bitstream/download/:bitstream
    * :bitstream: uuid of bitstream
    * returns BINARY data 

***  

## Browse to inaccessible community/collection
* Browse a community or collection page, retrieve relevant resources
* Get core metadata data for community/collection (name, handle)
  * GET /api/core/dso/:node
    * :node = community/collection uuid
    * returns [MinimalDSO](objectSchema.md#minimaldso)
      * status fields within the object indicate that it is inaccessible
* Get NodeContext for the community/collection
  * GET /api/node-context/:node
    * :node: "top" or repo uuid  
    * :depth: 0 to pull all community descendants
    * returns [NodeContext](objectSchema.md#nodecontext)


***

## Browse to inaccessible item
* Browse to an item page
* Get core metadata data for item (name, handle)
  * GET /api/core/dso/:node
    * :node = item uuid
    * returns [MinimalDSO](objectSchema.md#minimaldso)
      * status fields within the object indicate that it is inaccessible
* Get breadcrumb data
  * GET /api/core/hierarchy/ancestors/:node
    * :node = item uuid
    * returns Array of [MinimalDSO](objectSchema.md#minimaldso)

***

## Attempt to Download Bitstream (inaccessible to user)
  * GET /api/bitstream/download/:bitstream
    * :bitstream: uuid of bitstream
    * returns HTTP error code if inaccessible
  
***

## Create Community
* POST /api/core/community/:node/subcommunity
  * :node: parent community uuid
    * or "top" or repo uuid for top level communities
  * Payload: Array of [Metadata](objectSchema.md#metadata)
    * Should a Community object be passed instead?
  * Returns [Community](objectSchema.md#community)
  
***

## Edit Community
* PUT /api/core/community/:node
  * :node: community uuid
  * Payload: Array of [Metadata](objectSchema.md#metadata)
    * Should a Community object be passed instead?
  * Returns [Community](objectSchema.md#community)

***

## Delete Community
* DELETE /api/core/community/:node
  * :node: community uuid
  * Returns HTTP Status

***

## Add Community Policies
* POST /api/core/community/:node/policy
  * :node: community uuid
  * Payload: [Policy](objectSchema.md#policy)
  * Returns: [Policy](objectSchema.md#policy)

***

## Delete Community Policy
* DELETE /api/core/policy/:policy_id
  * :policy_id: policy uuid

***

## Edit Community Policy
Should policies be edited with the community or in a separate transaction?
* POST /api/core/policy/:policy_id
  * :policy_id: policy uuid
  * Payload: [Policy](objectSchema.md#policy)
  * Returns: [Policy](objectSchema.md#policy)

***

## Create Collection
* POST /api/core/community/:node/collection
  * :node: community uuid
  * Payload: Collection [Collection](objectSchema.md#collection)
    * Array of [Metadata](objectSchema.md#metadata)
    * Content Source Details
    * Workflow and template attributes
  * Returns [Collection](objectSchema.md#collection)

***

## Edit Collection Metadata
* PUT /api/core/collection/:node
  * :node: collection uuid
  * Payload: Collection [Collection](objectSchema.md#collection)
  * Returns [Collection](objectSchema.md#collection)

***

## Add Collection Policies
* POST /api/core/collection/:node/policy
  * :node: collection uuid
  * Payload: [Policy](objectSchema.md#policy)
  * Returns: [Policy](objectSchema.md#policy)

***

## Delete Collection Policy
* DELETE /api/core/policy/:policy_id
  * :policy_id: policy uuid

***

## Edit Collection Policy
Should policies be edited with the collection or in a separate transaction?
* POST /api/core/policy/:policy_id
  * :policy_id: policy uuid
  * Payload: [Policy](objectSchema.md#policy)
  * Returns: [Policy](objectSchema.md#policy)

***

## Curate Collection
* POST /api/core/collection/:coll/curate
  * :coll: collection uuid
  * Payload: [CurationSpec](objectSchema.md#curationspec)
    * Task Name
    * Parameter
  * Returns: [CurationResult](objectSchema.md#curationresult)

***

## Queue Curate Collection
* POST /api/core/collection/:coll/queue-curate
  * :coll: collection uuid
  * Payload: [Policy](objectSchema.md#policy)
  * Returns: [Policy](objectSchema.md#policy)

***

## Submit New Item to A Collection
* POST /api/core/collection/:coll/submit
  * :coll: collection uuid
  * Payload: [Item](objectSchema.md#item)
  * Returns: [Item](objectSchema.md#item)

***

## Edit Item in Workflow
* PUT /api/core/item/:item
  * :item: item uuid
  * Payload: [Item](objectSchema.md#item)
  * Returns: [Item](objectSchema.md#item)

***

## Review Item in Workflow
* POST /api/core/item/:item/workflow
  * :item: item uuid
  * Payload: ?
  * Returns: [Item](objectSchema.md#item)

***

## Accept Item License
* POST /api/core/item/:item/workflow
  * :item: item uuid
  * Payload: ?
  * Returns: [Item](objectSchema.md#item)

***

## Cancel Item Workflow
* POST /api/core/item/:item/workflow
  * :item: item uuid
  * Payload: ?
  * Returns: [Item](objectSchema.md#item)

***

## Edit Item Metadata
* PUT /api/core/item/:item
  * :item: item uuid
  * Payload: [Item](objectSchema.md#item)
  * Returns: [Item](objectSchema.md#item)

***

## Add Bitstream to Item
* POST /api/core/item/:item/Bitstream
  * :item: item uuid
  * Payload: [Bitstream](objectSchema.md#bitstream)
    * Does binary upload need to occur separately?
  * Returns: [Bitstream](objectSchema.md#bitstream)

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
