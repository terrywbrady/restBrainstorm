# Core Object Types
## DSO
* uuid: uuid
* name: String
* type: enum of DSO
* handle: String
* accessible: enum of accessibility summary (for current user)

## Repository
## Community
## Collection
## Item
## Bundle
## Bitstream
## Metadata

# Brainstorm Object Types

# Browse

# Hierarchy
* node: DSO (repo, community, collection)  
* children: Array of Hierarchy 

# Property
* module - String
* name - String
* dataType - Number, String, Array, Date, Map
* value - Object

# Option
* name - nmtoken string to be passed as a URL
* desecription - String describing the option

# Facet
* facetName - String
* facetType - Value sorted, alpha sorted
* moreUrl - Url to retrieve more values
* facetValues - Array
  * valueName - String
  * valueCount - Number
  * url - url for facet?

# Action
* name - String - action name
* actionType - enum categorizing action behavior
* url - Url to invoke action

* Examples
  * Admin Action (Create, Edit, Export)
  * Workflow Action (Submit)
  * Aux Action (Usage stats)
