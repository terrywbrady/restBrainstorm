# Potential Call Sequences with REST Api

### Main Page Load
* Get Welcome Message
  * /api/core/config/:prop-name
    * :prop-name = welcome
* Get List of Top Communities
  * /api/core/hierarchy/:node/child-nodes
    * :node = top or repo
* Get Recent Items
  * /api/discovery/:node/recent-items
    * :node = top or repo
* Get Browse Options for whole repo
  * /api/discovery/:node/browse-options
    * :node = top or repo
* Get Browse Options for whole repo
  * /api/discovery/:node/facets
    * :node = top or repo
  
### Community-List Page
*
