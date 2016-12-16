
# Details of api calls

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




