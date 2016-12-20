
# Details of api calls (based on [dataFlows.md](dataFlows.md))

## Global Parameters
* lang - Requests will default to repo's primary lang, if this is provided language specific replacements will be injected

## Config Properties
  * GET /api/core/config/:prop-group/:prop-name
    * :prop-group = 
    * :prop-name = 
    * returns [Property](objectSchema.md#property)

## Core Objects
* Get core metadata data for community/collection (name, handle)
  * GET /api/core/dso/:node
    * :node = community/collection uuid
    * returns [MinimalDSO](objectSchema.md#minimaldso)
* Get descriptive metadata data for community/collection
  * GET /api/core/metadata/:node
    * :node = community/collection uuid
    * returns Array of [Metadata](objectSchema.md#metadata)
* Handle
  * GET /api/core/handle/:prefix/:suffix
* Repository
  * GET /api/core/repository
  * POST /api/core/repository/community
* Community
  * GET    /api/core/community/:node
  * POST   /api/core/community/:node/community
  * POST   /api/core/community/:node/collection
  * POST   /api/core/community/:node/policy
  * PUT    /api/core/community/:node
  * DELETE /api/core/community/:node
* Collection
  * GET    /api/core/collection/:node
  * POST   /api/core/collection/:node/submit
  * POST   /api/core/collection/:node/policy
  * POST   /api/core/collection/:node/curate
  * POST   /api/core/collection/:node/queue-curate
  * PUT    /api/core/collection/:node
  * DELETE /api/core/collection/:node
* Item
  * GET    /api/core/item/:node
  * POST   /api/core/item/:node/bitstream
  * POST   /api/core/item/:node/policy
  * POST   /api/core/item/:node/workflow
  * POST   /api/core/item/:node/ownership
  * PUT    /api/core/item/:node
  * DELETE /api/core/item/:node
* Bitstreams
  * GET /api/core/item/:item/bitstream/:bundle/:num
    * :item = item uuid
    * :bundle - defaults to ORIGINAL
    * :num = 1 to pull primary bitstream, 0 to pull all, n to paginate
    * ?associated-bundles - defaults to THUMBNAIL - a link to associated bitstreams will be returned with an original bitstream
    * returns array of [Bitstream](objectSchema.md#bitstream)
  * GET /api/bitstream/download/:bitstream
    * :bitstream: uuid of bitstream
    * returns BINARY data 

## Authorization Policies
  * GET    /api/authorize/policy/:uuid
  * POST   /api/authorize/policy/:uuid
  * PUT    /api/authorize/policy/:uuid
  * DELETE /api/authorize/policy/:uuid

## Node Context - Browse
* Get Context Options for Current Node
  * GET /api/node-context/:node 
    * :node = "top" or repo uuid
    * ?depth: Number.  Pull n levels of descendants or 0 for all.  Default: 0 
    * returns [NodeContext](objectSchema.md#nodecontext) 
  * Get Browse Options for whole repo
    * GET /api/discovery/:node/browse-options
      * :node = "top" or repo uuid
      * returns Array of [Option](objectSchema.md#option)
  * Get Available Actions for the Node (create community)
    * GET /api/actions/:node
      * :node = "top" or repo uuid
      * returns Array of [Action](objectSchema.md#action)

## Hierarchy
  * Get breadcrumb data - returns nothing but a descriptive name at the top level
    * GET /api/core/hierarchy/ancestors/:node
      * :node = Community/Collection uuid  
      * returns Array of [MinimalDSO](objectSchema.md#minimaldso)
  * Get List of Top Communities
    * GET /api/core/hierarchy/descendants/:node/:depth
      * :node = "top" or repo uuid
      * ?depth: Number.  Pull n levels of descendants or 0 for all.  Default: 0 
      * returns [Hierarchy](objectSchema.md#hierarchy) containing only top level communities

## Discovery
  * Get Facet Options for whole repo
    * GET /api/discovery/:node/facets
      * :node = "top" or repo uuid
      * returns Array of [Facet](objectSchema.md#facet)
  * GET /api/discovery/browse/:node/:browse-mode
    * :node = "top" or repo uuid
    * :browse-mode = default - likely recent items
    * ?page - defaults to 0
    * ?size - defaults to default page size for node
    * returns array of [Item](objectSchema.md#item)
* Get Related Items
  * GET /api/discovery/:node/related-items
    * :node = item uuid
    * returns array of [Item](objectSchema.md#item)
* Search repository for items
  * POST /api/discovery/:node/search
    * :node = "top" or repo uuid or comm/coll uuid
    * ?page = page number
    * ?size = page size
    * ?sort-mode = choose from available sort options, the default sort will be used if not specified
    * Payload: solr query for "search" repo, may include advanced search text and facet values
    * returns [NodeContext](objectSchema.md#nodecontext) with search results and facets tailored to hits

## Administer People/Groups
* Administer people
  * GET    /api/eperson/eperson/:uuid
  * GET    /api/eperson/eperson/:email
  * POST   /api/eperson/eperson
  * PUT    /api/eperson/eperson/:uuid
  * DELETE /api/eperson/eperson/:uuid
* Administer groups
  * GET    /api/eperson/epersongroup/:uuid
  * POST   /api/eperson/epersongroup
  * PUT    /api/eperson/epersongroup/:uuid
  * DELETE /api/eperson/epersongroup/:uuid
  
## Registries
* Administer schema registry
  * GET    /api/registry/schema/:uuid
  * GET    /api/registry/schema/:prefix
  * POST   /api/registry/schema
  * PUT    /api/registry/schema/:uuid
  * DELETE /api/registry/schema/:uuid
* Administer metadata field registry
  * GET    /api/registry/schema/:prefix/metadata-field/:element+qualifier
  * GET    /api/registry/metadata-field/:uuid
  * POST   /api/registry/schema/:uuid/metadata-field
  * POST   /api/registry/schema/:prefix/metadata-field
  * PUT    /api/registry/metadata-field/:uuid
  * DELETE /api/registry/metadata-field/:uuid
* Administer format registry
  * GET    /api/registry/format/:uuid
  * GET    /api/registry/format/:mime
  * POST   /api/registry/format
  * PUT    /api/registry/format/:uuid
  * DELETE /api/registry/format/:uuid
  
## Bulk Modification
* Initiate bulk metadata edit
  * POST /api/app/bulk-metadata
    * ?preview: boolean
    * Payload: CSV
* Initiate bulk ingest
  * POST /api/app/bulk-ingest/:coll_uuid
    * Payload: Zip file of ingest folders

## Filter Items (by admin properties as opposed to end user search)
* Find Withdrawn items
  * POST /api/filter/item
* Find Private items
  * POST /api/filter/item
* Metadata query?
  * POST /api/filter/item
* Configurable Workflows checks like Sherpa
  * POST /api/plugin/sherpa

## General (pulled from prior api)
* GET  / - Return api overview
* GET  /api - Return api overview
* GET  /api/test - Return the string "REST api is running" for testing purposes.
* POST /api/login - Method for logging into the DSpace RESTful API.
* POST /api/logout - Method for logging out of the DSpace RESTful API. 

# Review of DSpace package list to identify candidate endpoints
Which of these packages will require the creation of an endpoint?

DSpace packages without REST endpoints
* Checksum checker - assume this is a background process that will not run via rest
  * Checksum data may be retrievable for an object
* What crosswalks will need to be exposed via rest?
* Packager - will run as a background process, no REST interface
* org.dspace.disseminate?
* org.dspace.embargo - will be invoked via submission
* events -backend
* org.dspace.google?
* harvest - backend
* rdf ? unsure how rest would interact
* search / indexer - backend.  Search exposed via discovery.  Index invoked by event system or curation.
  * see also org.dspace.text
* storage - backend

Other actions that will be needed
* /api/submit - To support item submission and workflow
  * Question: is the existing back end configuration still applicable for a rest based workflow, or would more of this move into the UI?
  * See also org.dspace.workflow and org.dspace.xmlworkflow
* /api/admin - To support dso maintainance and authorization of dso objects
* /api/authenticate - To authenticate a rest api user
* /api/authorize - To communicate authorization policies for a dso
* /api/authority - To support authority control for metadata
* /api/license - display/accept relevant license for a dso
* /api/curate - invoke curation tasks, queue curation tasks, display curation results
* /api/eperson - manage eperson, eperson groups
* /api/handle - (if handle functions are not part of /api/core)
* /api/identifier - doi and ezid
* /api/statistics - log usage.  query usage
  * See also org.dspace.usage 
* /api/plugin - register and invoke plugin behavior for items
* versioning - part of /api/core/item?




