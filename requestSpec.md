
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
  
Other actions
* /api/submit
* /api/admin
* /api
