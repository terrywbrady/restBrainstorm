
# Details of api calls (based on [dataFlows.md](dataFlows.md))

## Global Parameters
* lang - Requests will default to repo's primary lang, if this is provided language specific replacements will be injected

Retrieve system properties
  * GET  /api/core/config/:prop-group

Retrieve DSpace core objects
  * GET  /api/core/hierarchy/ancestors/:node
  * GET  /api/core/hierarchy/descendants/:node/:depth
  * GET  /api/core/hierarchy/browse/:node
  * GET  /api/core/dso/:node
  * GET  /api/core/metadata/:node
  * GET  /api/core/bitstreams/:node/:bundle/:num

Search Repository and Use Search Index for Related Items
  * GET  /api/discovery/:node/browse-options
  * GET  /api/discovery/:node/facets
  * GET  /api/discovery/:node/related-items
  * POST /api/discovery/:node/search
  * GET  /api/discovery/:node/search/facets
  * GET  /api/discovery/:node/sort-modes
  * GET  /api/discovery/:node/search-filters
  
Retrieve all relevant data associated with a browse action
  * GET  /api/browse/:node/:browse-mode
  
Retrieve action options for an object
  * GET  /api/actions/:node

# Notes pulled from DSpace 6 api

## General (pulled from prior api)
* GET  / - Return api overview
* GET  /api - Return api overview
* GET  /api/test - Return the string "REST api is running" for testing purposes.
* POST /api/login - Method for logging into the DSpace RESTful API.
* POST /api/logout - Method for logging out of the DSpace RESTful API. 

## DSO (pulled from prior api)
* Community
  * GET  /api/core/communities
  * POST - Create a top level community
  * POST - Create a subcommunity
  * PUT  - Update a community
  * DEL  - Delete the specified community.
  * Question: do we delete hierarchical links or is that only done by deleting a child object?
  * POST - Change ancestor for a community
* Collections
  * GET  /api/core/collections
  * POST - Create a collection within a community
  * PUT  - Update a collection
  * DEL  - Delete a collection
  * POST - Start a submission within a collection
* Items (
  * GET  /api/core/items
  * POST - Find items by the specified metadata value.
    * What types of changes need an independent endpoint in order to allow for clean authorization?
  * PUT  - update an item
  * DEL  - Delete the specified item.
* Bitstream
  * GET  /api/core/bitstream
  * PUT
  * DEL
  * POST add a new bitstream to a bundle
  * Do bundles have separate endpoints, or are bundles created and removed as needed?
* Schema Registry
  * GET /registries/schema - Return the list of metadata schemas in the registry
  * GET /registries/schema/{schema_prefix} - Returns the specified metadata schema
  * GET /registries/schema/{schema_prefix}/metadata-fields/{element} - Returns the metadata field within a schema with an unqualified element name
  * GET /registries/schema/{schema_prefix}/metadata-fields/{element}/{qualifier} - Returns the metadata field within a schema with a qualified element name
  * POST /registries/schema/ - Add a schema to the schema registry
  * POST /registries/schema/{schema_prefix}/metadata-fields - Add a metadata field to the specified schema
  * GET /registries/metadata-fields/{field_id} - Return the specified metadata field
  * PUT /registries/metadata-fields/{field_id} - Update the specified metadata field
  * DELETE /registries/metadata-fields/{field_id} - Delete the specified metadata field from the metadata field registry
  * DELETE /registries/schema/{schema_id} - Delete the specified schema from the schema registry
* Metadata
  /api/core/metadata - construct a metadata query
* Filters (DSpace 6)
  This concept could be useful to incorporate into the api once we know the layout of the new api calls

# Review of DSpace package list to identify candidate endpoints

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




